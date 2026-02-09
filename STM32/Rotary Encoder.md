
# STM32 Timer Encoder Interface — Summary Notes

## Quadrature Encoder Working Principle

- Encoder provides **two digital signals**: **Channel A (TI1)** and **Channel B (TI2)**
    
- Signals are **90° phase shifted**
    
- **Direction** determined by which signal leads:
    
    - A leads B → Clockwise
        
    - B leads A → Counter-Clockwise
        
- STM32 timer hardware:
    
    - Detects direction automatically
        
    - Increments / decrements `TIMx_CNT`
        
    - No CPU involvement during counting
        

---

##  Encoder Decoding Types

| Decoding | Counts per cycle | Description                       |
| -------- | ---------------- | --------------------------------- |
| X1       | 1                | One edge only (not used in STM32) |
| X2       | 2                | One channel edges                 |
| X4       | 4                | Both channels, all edges          |

---

## Encoder Modes (SMCR.SMS)

| SMS bits | Mode           | Description                         | Resolution |
| -------- | -------------- | ----------------------------------- | ---------- |
| `001`    | Encoder Mode 1 | Count TI1 edges, direction from TI2 | X2         |
| `010`    | Encoder Mode 2 | Count TI2 edges, direction from TI1 | X2         |
| `011`    | Encoder Mode 3 | Count TI1 + TI2 edges               | **X4**     |

---

## Encoder Mode Working Summary

###  Encoder Mode 1

- Counts **Channel A edges**
    
- Direction sensed from **Channel B level**
    
- Medium resolution
    
- Less sensitive to noise
    

###  Encoder Mode 2

- Counts **Channel B edges**
    
- Direction sensed from **Channel A level**
    
- Same resolution as Mode 1
    
- Inputs swapped
    

###  Encoder Mode 3 (Most used)

- Counts **both A and B edges**
    
- Maximum resolution
    
- Direction detected from phase relationship
    

---

##  Timer Registers Used in Encoder Interface

| Register                    | Purpose                       |
| --------------------------- | ----------------------------- |
| `RCC_APB1ENR / RCC_APB2ENR` | Enable timer clock            |
| `GPIOx_MODER`               | Set encoder pins to AF        |
| `GPIOx_AFR`                 | Select TIM alternate function |
| `GPIOx_PUPDR`               | Enable pull-ups               |
| `TIMx_SMCR`                 | Select encoder mode           |
| `TIMx_CCMR1`                | Configure CC1 & CC2 as inputs |
| `TIMx_CCER`                 | Input polarity selection      |
| `TIMx_CNT`                  | Encoder position counter      |
| `TIMx_ARR`                  | Counter limit                 |
| `TIMx_CR1`                  | Enable timer                  |

---

##  Important Bit Fields

### Encoder Mode Selection

```c
TIMx->SMCR.SMS = 001 / 010 / 011;
```

### Capture Compare Input Selection

```c
CC1S = 01 → TI1
CC2S = 01 → TI2
```

### Input Filter (Debounce)

```c
ICxF = 6 → fCK_INT / 32, 8 samples
```

### Counter Enable

```c
TIMx->CR1 |= TIM_CR1_CEN;
```

---

##  KY-040 Practical Notes

|Parameter|Value|
|---|---|
|Physical detent|1 click|
|Encoder pulses|4 per click|
|Required mode|Encoder Mode 3|
|Software scaling|`diff >= 4`|

---

## Advantages of STM32 Encoder Interface

- No interrupts required
    
- Zero CPU load during counting
    
- Automatic direction detection
    
- Works with bare-metal and RTOS
    
- High accuracy and reliability
    

---

##  Typical Applications

- Menu navigation
    
- Motor position control
    
- Speed/RPM measurement
    
- Industrial encoders
    
- Human-machine interfaces
    

---

##  Common Mistakes

|Mistake|Effect|
|---|---|
|No pull-ups|Unstable count|
|No input filter|Noise jumps|
|Wrong AF|No counting|
|Wrong encoder mode|Half resolution|

---



Great question 👍 — this is a **very professional habit** to build early.

Below are **best practices + ready-to-use commit messages** specifically for **your encoder work**.

---

## ✅ General Rules for a Good Commit Message

### 1️⃣ Use **imperative mood**

Think: _“This commit will …”_

❌ `Added encoder code`  
✅ `Add TIM1 quadrature encoder support`

---

### 2️⃣ Keep subject ≤ **50 characters**

Short, clear, searchable.

---

### 3️⃣ Explain **why**, not just what

Code shows _what_, commit message explains _why_.

---

### 4️⃣ One logical change per commit

Your change = encoder feature → one commit ✔

---

## 🔷 Recommended Commit Message Format

```
<type>: <short summary>

<optional detailed explanation>
```

---

## 🔷 Suggested Types (Common Convention)

|Type|Use when|
|---|---|
|feat|New feature|
|fix|Bug fix|
|refactor|Code structure change|
|docs|Comments / documentation|
|test|Tests added|
|chore|Cleanup / build changes|

---

## 🟢 BEST COMMIT MESSAGE FOR YOUR CASE (Recommended)

### ✔ If this is a **new feature**

```
feat: add TIM1 quadrature encoder interface (X4)

Configure TIM1 in encoder mode 3 with GPIO AF setup,
input filtering, and software scaling for KY-040 encoder.
Includes detailed register-level comments for future reference.
```

---

## 🟡 If main change is **documentation/comments**

```
docs: add detailed comments for STM32 encoder interface

Explain TIM1 encoder mode selection, CC/TI mapping,
input polarity, filtering, and X4 decoding behavior.
```

---

## 🔵 If this is part of learning / experimentation repo

```
feat: implement rotary encoder using TIM1 encoder mode

Use hardware quadrature decoding with X4 resolution
and debounce filtering for KY-040 mechanical encoder.
```

---

## 🔴 If this is a refactor of earlier code

```
refactor: clean up TIM1 encoder initialization

Reorganize GPIO and timer setup and add comprehensive
comments explaining encoder hardware behavior.
```

---

## 🔑 Ultra-Short Version (Still Acceptable)

```
feat: TIM1 quadrature encoder (X4, KY-040)
```

---

## 🚫 Avoid These Commit Messages

❌ `encoder working`  
❌ `final code`  
❌ `updated`  
❌ `changes done`

These give **zero context** later.

---

## 🧠 Pro Tip (Very Important)

Imagine **6 months later**, you ask:

> “Why did I change this?”

A good commit message should answer that **without opening the code**.

---

## ✅ My Strong Recommendation (Use This)

If I were reviewing your repo, I’d want to see:

```
feat: add TIM1 quadrature encoder interface (X4)

Hardware-based quadrature decoding using STM32 TIM1
encoder mode 3 with strong input filtering for KY-040.
Includes register-level documentation and software
scaling for logical step control.
```

---

If you want, I can also help you:

- 📌 Split this into **multiple clean commits**
    
- 🧾 Write **GitHub PR description**
    
- 🧠 Create **commit message template**
    
- 🏷 Tag releases professionally
    

Just say 👍


```
feat: add ADC_CH0 POT interface (PA0)

Potentiometer (10kohm) interfacing adc code with 480 sampling cycle.
```