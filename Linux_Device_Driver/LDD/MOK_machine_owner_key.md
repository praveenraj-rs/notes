
---
# 🔐 Linux Device Driver Development using MOK (Secure Boot ON)

## 🎯 Goal

- ✅ Keep **Secure Boot ON**
    
- ✅ Load **your own kernel modules (.ko)**
    
- ✅ Follow **professional / industry-safe practice**
    
---

## 🧠 Big Picture (1-Minute Mental Model)

Secure Boot → blocks **unsigned kernel code**

Solution:

1. Create **your own signing key**
    
2. Tell **Ubuntu to trust it** (MOK)
    
3. **Sign every kernel module** you build
    

Secure Boot **never gets disabled**.

---

# ✅ STEP-BY-STEP (PROPERLY ORDERED)

---

## 🟢 STEP 1: Create MOK signing key (ONE-TIME)

📍 Do this **once per machine**.

```bash
mkdir -p ~/mok
cd ~/mok
```

Create key + certificate:

```bash
openssl req -new -x509 -newkey rsa:2048 \
-keyout MOK.key -out MOK.crt -nodes -days 3650 \
-subj "/CN=My Linux Driver/"
```

### You get:

- 🔐 `MOK.key` → **PRIVATE KEY (protect this)**
    
- 🔑 `MOK.crt` → **PUBLIC certificate**
    

🔒 **Security note**

```bash
chmod 600 MOK.key
```

---

## 🟢 STEP 2: Enroll public key into MOK (ONE-TIME)

```bash
sudo mokutil --import ~/mok/MOK.crt
```

- Set a **temporary password**
    
- Reboot when asked
    

---

## 🟢 STEP 3: Enroll key in MOK Manager (ONE-TIME)

On reboot → **Blue screen (MOK Manager)**:

1. **Enroll MOK**
    
2. **Continue**
    
3. **Yes**
    
4. Enter password
    
5. Reboot again
    

✅ Ubuntu now **trusts your signing key**

---

## 🟢 STEP 4: Verify Secure Boot + MOK (OPTIONAL BUT RECOMMENDED)

```bash
mokutil --sb-state
```

Expected:

```
SecureBoot enabled
```

Check enrolled keys:

```bash
mokutil --list-enrolled | grep "My Linux Driver"
```

---

## 🟢 STEP 5: Write & compile your kernel module (NORMAL)

Example:

```bash
make
```

Output:

```
my_driver.ko
```

⚠️ **At this stage the module is UNSIGNED**

---

## 🟢 STEP 6: Sign the kernel module (EVERY BUILD)

```bash
sudo /usr/src/linux-headers-$(uname -r)/scripts/sign-file \
sha256 ~/mok/MOK.key ~/mok/MOK.crt my_driver.ko
```

✔ This embeds a cryptographic signature into `.ko`

---

## 🟢 STEP 7: Verify module signature (RECOMMENDED)

```bash
modinfo my_driver.ko | grep signer
```

Expected:

```
signer: My Linux Driver
```

---

## 🟢 STEP 8: Load the driver

```bash
sudo insmod my_driver.ko
```

or (preferred if using `/lib/modules`):

```bash
sudo modprobe my_driver
```

---

## 🟢 STEP 9: Verify module is loaded

```bash
lsmod | grep my_driver
```

Kernel log:

```bash
dmesg | tail
```

Expected:

- ✅ No “Operation not permitted”
    
- ✅ No “Module verification failed”
    

---

# 🔁 ONE-TIME vs EVERY-TIME (IMPORTANT)

### 🧱 ONE-TIME ONLY

✔ Create MOK key  
✔ Enroll key with `mokutil`  
✔ MOK Manager confirmation

---

### 🔁 EVERY TIME YOU BUILD

✔ Compile driver  
✔ **Sign `.ko`**  
✔ Load module

---

# ⚠️ Common Mistakes (Avoid These)

❌ Forgetting to sign after rebuild  
❌ Losing `MOK.key`  
❌ Using wrong kernel headers  
❌ Copying `.ko` without re-signing  
❌ Using spaces instead of TAB in kernel Makefile

---

# 🧠 Why Windows + Valorant Still Works

- Secure Boot stays **ON**
    
- Firmware trust chain unchanged
    
- Windows Boot Manager untouched
    
- Riot Vanguard is satisfied
    

👉 This is the **only correct way** on dual-boot systems.

---

# 🟢 Professional Verdict

> ✅ **This is the correct, safe, and industry-approved way to develop Linux kernel drivers with Secure Boot enabled.**

You are doing this **the right way** 👍

---

If you want next, I can:

- Automate signing in your **Makefile**
    
- Show **DKMS + MOK workflow**
    
- Explain **kernel signature internals**
    
- Help you design a **production-safe key strategy**
    

Just tell me 🔧


This error is **very common** and **not dangerous** 👍  
It happens because **`mokutil` expects the certificate in DER format**, but your `MOK.crt` is currently in **PEM format**.

Let’s fix it **cleanly and correctly**.

---

## ❌ The Error (What it means)

```
Abort!!! /home/praveenrajrs/mok/MOK.crt is not a valid x509 certificate in DER format
```

### Why this happens

- `openssl req -x509` creates a **PEM** certificate by default
    
- `mokutil --import` requires **DER-encoded X.509**
    

So `mokutil` rejects the file.

---

## ✅ Correct Fix (2 Commands)

### 🔹 Step 1: Convert PEM → DER

Run this **inside your `~/mok` directory**:

```bash
openssl x509 -in MOK.crt -outform DER -out MOK.der
```

Now you have:

- `MOK.crt` → PEM (keep it)
    
- `MOK.der` → DER (used for MOK enrollment)
    

---

### 🔹 Step 2: Import the DER certificate

```bash
sudo mokutil --import ~/mok/MOK.der
```

- Set a **temporary password**
    
- Reboot
    

---

## 🔵 Enroll Key on Reboot (Reminder)

On reboot:

1. **Enroll MOK**
    
2. **Continue**
    
3. **Yes**
    
4. Enter password
    
5. Reboot again
    

---

## ✅ Verify After Boot

```bash
mokutil --list-enrolled | grep "My Linux Driver"
```

And:

```bash
mokutil --sb-state
```

Expected:

```
SecureBoot enabled
```

---

## 🧠 Why DER is required (simple explanation)

|Format|Purpose|
|---|---|
|PEM (`.crt`)|Human-readable, OpenSSL, signing|
|DER (`.der`)|Binary, firmware-friendly, **MOK enrollment**|

UEFI firmware **cannot parse PEM**, so DER is mandatory.

---

## ⚠️ DO NOT delete these files

Keep all of them:

- 🔐 `MOK.key` → private (MOST IMPORTANT)
    
- 🔑 `MOK.crt` → signing reference
    
- 🔑 `MOK.der` → MOK enrollment
    

---

## ✅ One-line summary

> `mokutil` failed because your certificate was PEM; converting it to DER fixes the issue permanently.

---

If you want next, I can:

- Modify your **Makefile to auto-sign**
    
- Show how to **revoke a MOK key**
    
- Explain **“module verification failed” errors**
    
- Help with **DKMS + Secure Boot**
    

Just tell me 👍

```Makefile
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