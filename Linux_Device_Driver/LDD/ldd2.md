# ✅ PART 1: WHAT THIS CHAPTER TEACHES (Big Picture)

This chapter teaches you:

1. ✅ What a **kernel module** is
2. ✅ Difference between **user programs & kernel modules**
3. ✅ How to write your **first Linux kernel module**
4. ✅ How to **compile, load, unload** it
5. ✅ What happens inside the kernel
6. ✅ How to pass parameters
7. ✅ How module loading really works

📌 This chapter does NOT deal with hardware yet
→ It prepares you for **real driver development**

---

# ✅ PART 2: WHAT IS A KERNEL MODULE?

### ✔ Definition

A **kernel module** is:

* A piece of code
* Loaded into the Linux kernel at runtime
* Extends kernel functionality

### ✔ Why modules exist?

Without modules:

* You must rebuild kernel every time
* Slow development
* Hard to test

With modules:

* Load → test → unload
* No reboot required
* Faster development

---

# ✅ PART 3: HELLO WORLD KERNEL MODULE (IMPORTANT)

### 📌 This is your FIRST driver

### 📄 File: `hello.c`

```c
#include <linux/init.h>
#include <linux/module.h>

MODULE_LICENSE("GPL");

static int __init hello_init(void)
{
    printk(KERN_ALERT "Hello, world\n");
    return 0;
}

static void __exit hello_exit(void)
{
    printk(KERN_ALERT "Goodbye, cruel world\n");
}

module_init(hello_init);
module_exit(hello_exit);
```

---

## 🔍 EXPLANATION LINE BY LINE

### 1️⃣ Header files

```c
#include <linux/init.h>
#include <linux/module.h>
```

Required for:

* module loading
* init / exit macros

---

### 2️⃣ License

```c
MODULE_LICENSE("GPL");
```

✔ Tells kernel this is **open-source**
✔ Avoids kernel taint warning

---

### 3️⃣ Initialization function

```c
static int __init hello_init(void)
```

Runs when module is **loaded**

`__init` → kernel frees this memory after loading

---

### 4️⃣ printk()

```c
printk(KERN_ALERT "Hello, world\n");
```

Kernel version of `printf`

| Level      | Meaning       |
| ---------- | ------------- |
| KERN_ALERT | High priority |
| KERN_INFO  | Normal        |
| KERN_ERR   | Error         |

---

### 5️⃣ Exit function

```c
static void __exit hello_exit(void)
```

Runs when module is removed

---

### 6️⃣ Register functions

```c
module_init(hello_init);
module_exit(hello_exit);
```

Without these → kernel won’t call your code

---

# ✅ PART 4: HOW TO COMPILE & RUN (VERY IMPORTANT)

---

## 🧱 Step 1: Create files

```bash
mkdir hello_driver
cd hello_driver
```

Create file:

```bash
nano hello.c
```

Paste code.

---

## 🧱 Step 2: Create Makefile

📄 `Makefile`

```make
obj-m := hello.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```

### Makefile with MOK Signing
```sh
obj-m := hello.o

KDIR := /lib/modules/$(shell uname -r)/build
PWD  := $(shell pwd)

# MOK key paths
MOK_KEY := $(HOME)/mok/MOK.key
MOK_CRT := $(HOME)/mok/MOK.crt
SIGN_SCRIPT := $(KDIR)/scripts/sign-file

all:
	$(MAKE) -C $(KDIR) M=$(PWD) modules
	sudo $(SIGN_SCRIPT) sha256 $(MOK_KEY) $(MOK_CRT) hello.ko

clean:
	$(MAKE) -C $(KDIR) M=$(PWD) clean
```
---

## 🧱 Step 3: Compile module

```bash
make
```

If successful, you’ll get:

```
hello.ko
```

---

## 🧱 Step 4: Load module

```bash
sudo insmod hello.ko
```

Check output:

```bash
dmesg | tail
```

You’ll see:

```
Hello, world
```

---

## 🧱 Step 5: Remove module

```bash
sudo rmmod hello
```

Check:

```bash
dmesg | tail
```

Output:

```
Goodbye, cruel world
```

✅ You just ran a kernel module!

---

# ✅ PART 5: IMPORTANT CONCEPTS YOU MUST UNDERSTAND

---

## 🔹 1. Kernel Space vs User Space

| User Space       | Kernel Space        |
| ---------------- | ------------------- |
| printf()         | printk()            |
| malloc()         | kmalloc()           |
| Can crash itself | Can crash entire OS |
| Safe             | Dangerous           |

📌 Kernel has **no standard C library**

---

## 🔹 2. Why Kernel Programming is Hard

✔ No floating point
✔ Very small stack
✔ Must handle concurrency
✔ Crash = system crash
✔ No debugging tools like gdb

---

## 🔹 3. Module Loading Flow

```
insmod
   ↓
kernel allocates memory
   ↓
resolves symbols
   ↓
calls module_init()
```

---

## 🔹 4. Module Removal Flow

```
rmmod
   ↓
module_exit()
   ↓
memory freed
```

---

## 🔹 5. lsmod command

```bash
lsmod
```

Shows:

* Loaded modules
* Dependencies
* Usage count

---

# ✅ PART 6: MODULE PARAMETERS (IMPORTANT)

Example:

```c
static int howmany = 1;
static char *whom = "world";

module_param(howmany, int, 0444);
module_param(whom, charp, 0444);
```

Load with:

```bash
sudo insmod hello.ko howmany=5 whom="Linux"
```

Output:

```
Hello Linux
Hello Linux
Hello Linux
Hello Linux
Hello Linux
```

---

# ✅ PART 7: WHY MODULES ARE POWERFUL

✔ No reboot needed
✔ Can update drivers easily
✔ Supports dynamic hardware
✔ Safer testing
✔ Used by USB, WiFi, Audio, GPU

---

# ✅ PART 8: WHAT YOU SHOULD PRACTICE NOW

### ✅ Task 1

Modify hello module to print:

```
Hello from my Linux driver
```

### ✅ Task 2

Add module parameter:

```bash
insmod hello.ko count=5
```

### ✅ Task 3

Print:

* process ID
* process name

(using `current->pid`)

---

# 🎯 NEXT STEPS (VERY IMPORTANT)

Next chapter you should learn:

➡ Character Device Driver
➡ `open()`, `read()`, `write()`
➡ `/dev/mydevice`
➡ File operations
➡ Major & Minor numbers

---
