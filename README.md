## 📘 STM32 OLED I2C Interfacing (Register Level – No HAL)

This project demonstrates **interfacing a 128×64 OLED display (SSD1306)** with **STM32F446RE** using **pure register-level programming**.

🚫 No HAL
🚫 No CubeMX
✅ Bare-metal registers only

If you want to **understand how I2C really works inside STM32**, this project is your playground.

---

## 🎯 What This Project Does

* Initializes **I2C1** using STM32 registers
* Communicates with **SSD1306 OLED** over I2C
* Implements:

  * OLED initialization sequence
  * Screen clear
  * Cursor positioning
  * Character & string rendering
* Uses a **custom 6×8 ASCII font**
* Displays multiple strings on different OLED pages

---

## 🧰 Hardware Requirements

| Component | Description                |
| --------- | -------------------------- |
| MCU       | STM32F446RE (Nucleo)       |
| Display   | 128×64 OLED (SSD1306, I2C) |
| Interface | I2C                        |
| Wires     | Jumper wires               |

---

## 🔌 Pin Connections

| OLED Pin | STM32F446RE Pin |
| -------- | --------------- |
| VCC      | 3.3V            |
| GND      | GND             |
| SDA      | PB9 (I2C1 SDA)  |
| SCL      | PB8 (I2C1 SCL)  |

📌 **Note:**
PB8 & PB9 are configured as **AF4 Open-Drain with Pull-Up**, exactly how I2C expects.

---

## 🧠 Core Concepts Covered

This repo is not just about “making OLED work”—it teaches **how** it works.

### 1️⃣ SysTick Delay (Register Based)

```c
void delay_ms(uint32_t ms);
```

* Uses **SysTick timer**
* No HAL delay calls
* Accurate millisecond delays

---

### 2️⃣ I2C Initialization (Bare Metal)

```c
void I2C1_Init(void);
```

Configures:

* GPIOB alternate function
* Open-drain outputs
* APB1 clock for I2C
* Clock control, rise time, CCR

You’ll finally understand:

> “Why these I2C registers exist in the first place.”

---

### 3️⃣ Low-Level I2C Transactions

| Function        | Purpose                  |
| --------------- | ------------------------ |
| `I2C_Start()`   | Generate START condition |
| `I2C_Address()` | Send OLED slave address  |
| `I2C_Write()`   | Transmit data/command    |
| `I2C_Stop()`    | Generate STOP condition  |

This mirrors **actual I2C timing diagrams**, not abstract HAL calls.

---

### 4️⃣ OLED Control Logic

| Function           | Role                   |
| ------------------ | ---------------------- |
| `OLED_Command()`   | Send command byte      |
| `OLED_Data()`      | Send pixel data        |
| `OLED_Init()`      | SSD1306 initialization |
| `OLED_Clear()`     | Clear full screen      |
| `OLED_SetCursor()` | Page & column control  |

---

### 5️⃣ Font Rendering Engine

* Custom **6×8 ASCII font**
* Each character = 6 bytes
* Stored in Flash
* Drawn column-by-column

```c
void OLED_DrawChar(char c);
void OLED_DrawString(uint8_t x, uint8_t page, const char *str);
```

This teaches **how text is actually rendered on pixel displays**.

---

## 🖥️ Output Preview

The OLED displays:

```
STM32F446
STM32 OLED I2C
DANIEL RAJ.C
_____________
```

Each line is written on a different OLED **page**.

---

## ▶️ How to Run This Project

1. Open **STM32CubeIDE**
2. Create a **bare STM32 project**
3. Replace `main.c` with the provided code
4. Build & Flash
5. Power the board
6. Watch the OLED come alive ✨

---

## 🧩 Why Register Coding?

Let’s be real:

* HAL = fast results
* Registers = real understanding

This project helps you:

* Read reference manuals confidently
* Debug hardware issues faster
* Crack interviews that ask
  👉 *“How does I2C work internally?”*

---

## 🚀 Who This Repo Is For

* STM32 beginners stepping beyond HAL
* Embedded learners who want **strong fundamentals**
* Anyone preparing for **embedded interviews**
* Curious minds who love bare-metal control

---

## 📌 Future Enhancements (Ideas)

* Scrolling text
* Inverted display mode
* Bigger fonts
* Multi-line text wrapping
* I2C error handling

---

## 📜 License

This project is MIT- Licenced and free to use for **learning and experimentation**.

---

