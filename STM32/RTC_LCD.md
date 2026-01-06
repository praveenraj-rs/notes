```c
#include "stm32f4xx.h"
#include <stdint.h>
#include <string.h>
#include <stdlib.h>
#include <stdbool.h>
#include <stdio.h>

#define SysClk 25000000U 	// 25MHz HSE system clock frequency

#define B_LED 13U 			// PC13 Built-in LED
#define Btn 0U 				// PA0 push-btn active low

#define Tx1	9				// PA9 Tx UART1
#define Rx1 10				// PA10 Rx UART1

#define Magic_RTC_Value 0x143 // To prevent setting of time on reset

// Function Prototyping
void SystemClock_Init(void);

void B_LED_Init(void);
void Btn_Init(void);

void TIM3_Delay(uint16_t delay_ms);

void UART1_Init(void);
void UART1_Send_Char(char c);
void UART1_Send_Str(char *str);
char UART1_Receive_Char(void);
void UART1_Receive_Str(char *str);

void RTC_Init(void)
{
	// 1) Enable PWR clock and allow access to backup domain
	RCC->APB1ENR |= RCC_APB1ENR_PWREN;
	PWR->CR |= PWR_CR_DBP;

	// RTC->BKP0R = Magic_RTC_Value;

	// 2) (Optional but clean) Reset backup domain if changing clock source
	RCC->BDCR |= RCC_BDCR_BDRST;
	RCC->BDCR &= ~RCC_BDCR_BDRST;

	// 3) Enable LSI (internal ~32 kHz RC)
	RCC->CSR |= RCC_CSR_LSION;
	while(!(RCC->CSR & RCC_CSR_LSIRDY));   // wait for LSI ready

	// 4) Select LSI as RTC clock
	RCC->BDCR &= ~RCC_BDCR_RTCSEL;         // Clear RTCSEL bits
	RCC->BDCR |= RCC_BDCR_RTCSEL_1;        // 10: LSI selected as RTC clock

	// 5) Enable RTC
	RCC->BDCR |= RCC_BDCR_RTCEN;

	// 6) Disable write protection
	RTC->WPR = 0xCA;
	RTC->WPR = 0x53;

	// 7) Enter init mode
	RTC->ISR |= RTC_ISR_INIT;
	while(!(RTC->ISR & RTC_ISR_INITF));

	// 8) Set prescalers for LSI ~32 kHz
	// f_RTC = 32000 / ((PREDIV_A+1) * (PREDIV_S+1))
	// Choose PREDIV_A = 127, PREDIV_S = 249 → 32000 / (128*250) = 1 Hz
	RTC->PRER = (127 << RTC_PRER_PREDIV_A_Pos) |
				(249 << RTC_PRER_PREDIV_S_Pos);

	// 9) Set default time/date (same as your example)
	RTC->TR = 0x00104000;  // 15:30:00 (BCD)
	RTC->DR = 0x00251209;  // 2021-12-01 (BCD)

	// 10) Exit init mode
	RTC->ISR &= ~RTC_ISR_INIT;

	// 11) Re-enable write protection
	RTC->WPR = 0xFF;
}



int main(void)
{
	// Initialization
	SystemClock_Init(); 				// Selecting HSE 25MHz
	UART1_Init();						// UART1 initialization
	RTC_Init();

	char buffer[64];
	uint32_t tr;
	int hrs, min, sec;

	while (1)
	{
		tr = RTC->TR;

		hrs = ((tr >> 20) & 0x3)*10 + ((tr >> 16) & 0xF);
		min = ((tr >> 12) & 0x7)*10 + ((tr >>  8) & 0xF);
		sec = ((tr >>  4) & 0x7)*10 + ((tr >>  0) & 0xF);

		sprintf(buffer, "Time: %02d:%02d:%02d\r\n", hrs, min, sec);
		UART1_Send_Str(buffer);

		TIM3_Delay(1000);
	}
}


void SystemClock_Init(void)
{
   // Enable HSE
   RCC->CR |= RCC_CR_HSEON;
   while (!(RCC->CR & RCC_CR_HSERDY)) { /* Wait until ready */ }

   // Set Flash latency for 25 MHz (0 WS is fine)
   FLASH->ACR = FLASH_ACR_ICEN | FLASH_ACR_DCEN | FLASH_ACR_PRFTEN | FLASH_ACR_LATENCY_0WS;

   // Set AHB, APB1, and APB2 pre-scalers = 1
   RCC->CFGR &= ~(RCC_CFGR_HPRE | RCC_CFGR_PPRE1 | RCC_CFGR_PPRE2);
   RCC->CFGR |= RCC_CFGR_HPRE_DIV1 | RCC_CFGR_PPRE1_DIV1 | RCC_CFGR_PPRE2_DIV1;

   // Select HSE as system clock
   RCC->CFGR &= ~RCC_CFGR_SW;
   RCC->CFGR |= RCC_CFGR_SW_HSE;

   // Wait until HSE is used as system clock
   while ((RCC->CFGR & RCC_CFGR_SWS) != RCC_CFGR_SWS_HSE) { /* Wait */ }
}

void B_LED_Init(void)
{
	RCC->AHB1ENR |= RCC_AHB1ENR_GPIOCEN; 	// Enable GPIOC clock
	GPIOC->MODER &= ~(3U << (B_LED * 2));	// Clear register
	GPIOC->MODER |=  (1U << (B_LED * 2));  	// 01: Output mode
	GPIOC->OTYPER &= ~(1U << B_LED);		// Push-pull
	GPIOC->PUPDR &= ~(3U << (B_LED * 2));	// No pull-up or pull-down
	GPIOC->ODR |= (1<<B_LED);				// LED off
}

void Btn_Init(void)
{
   RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN;		// Enable GPIOA clock
   GPIOA->MODER &= ~(3U << (Btn * 2));    	// 00: Input mode
   GPIOA->PUPDR &= ~(3U << (Btn * 2));    	// Clear register
   GPIOA->PUPDR |= (1U << (Btn * 2));    	// Pull-up configuration
}

void TIM3_Delay(uint16_t delay_ms)
{
	 RCC->APB1ENR |= RCC_APB1ENR_TIM3EN;		// Enable TIM3 Clock

	 uint32_t prescaler = (SysClk / 1000) - 1;	// Timer clock = 1 KHz or 1ms
	 TIM3->PSC = prescaler - 1;					// Pre-scaler update

	 TIM3->ARR = delay_ms - 1;   			// Auto-reload 1 second delay (1ms * 999)
	 TIM3->CNT = 0;							// Reset the counter
	 TIM3->EGR |= (1 << 0);  				// Event generation

	 TIM3->SR &= ~ (1 << 0);  				// Clear update interrupt flag
	 TIM3->CR1 |= (1 << 0); 				// Enable Timer

	 while (!(TIM3->SR & (1 << 0))){} 		// Until UIF NEQ 1
	 TIM3->SR &= ~(1 << 0); 				//UIF is cleared manually
	 TIM3->CR1 &= ~(1 << 0); 				//CEN is cleared
}

void UART1_Init(void)
{
	 // Enable clocks for GPIOA and USART1
	 RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN;   // GPIOA clock enable
	 RCC->APB2ENR |= RCC_APB2ENR_USART1EN;  // USART1 clock enable

	 // Configure PA9 (TX1) and PA10 (RX1) as Alternate Function 7 (AF7)
	 GPIOA->MODER &= ~( (3U << (Tx1 * 2)) | (3U << (Rx1 * 2)) );  					// 00: Clear register
	 GPIOA->MODER |=  ( (2U << (Tx1 * 2)) | (2U << (Rx1 * 2)) );  					// 10: AF mode
	 GPIOA->AFR[1] &= ~( (0xFU << ((Tx1 - 8) * 4)) | (0xFU << ((Rx1 - 8) * 4)) );	// 00: Clear register
	 GPIOA->AFR[1] |=  ( (7U << ((Tx1 - 8) * 4)) | (7U << ((Rx1 - 8) * 4)) );  		// AF7 for USART1
	 GPIOA->OSPEEDR |= (3U << (Tx1 * 2)) | (3U << (Rx1 * 2));  						// High speed

	 // Configure USART1
	 USART1->CR1 = 0;  								// Disable before configuration
	 USART1->BRR = 0xA2C;  							// 9600 baud @25 MHz
	 USART1->CR1 |= (USART_CR1_TE | USART_CR1_RE);  // Enable TX, RX
	 USART1->CR1 |= USART_CR1_UE;                   // Enable USART1
}

void UART1_Send_Char(char c)
{
	while (!(USART1->SR & USART_SR_TXE));  // wait until TX buffer empty
	USART1->DR = (c & 0xFF);
}

void UART1_Send_Str(char *str)
{
	 while(*str)
	 {
		 UART1_Send_Char(*str++);
	 }
}

char UART1_Receive_Char(void)
{
   while (!(USART1->SR & USART_SR_RXNE));  // wait until data received
   return (char)(USART1->DR & 0xFF);
}

void UART1_Receive_Str(char *buffer)
{
   char c;
   uint16_t i = 0;
   do {
       c = UART1_Receive_Char();
       buffer[i++] = c;
   } while (c != '\n' && c != '\r');  	// until newline or carriage return
   buffer[i] = '\0';  					// null terminate
}

```