# 🕰️ ns32k-timewarp

```
───────────────────────────────────────────────
          n s 3 2 k   t i m e w a r p
───────────────────────────────────────────────
```

> *Revisiting 1980s 32-bit computing.*

---

## 💡 Background

In **1988** or thereabouts, I bought a **National Semiconductor Series 32000 Designer Kit** from Geoff Wood Electronics in Sydney, it featured the **NS32032** — one of the earliest true 32-bit microprocessors.  
It promised workstation-class performance at a hobbyist-friendly price.

Then life happened.

For **37 years**, it sat quietly in my *“when I get around to it”* pile — until I rediscovered the original chips while searching for something else.  
That moment sparked a question:

> **Could I bring this forgotten board back to life?**

This repository is the answer — a journey through time, silicon, and stubborn nostalgia.

---

## ⚙️ Project Overview

This project reconstructs a **functioning NS32032 system** using the surviving original parts from that long-lost designer kit.

All documentation was gone — no schematics, no manuals — so this required:

- 🔍 **Reverse-engineering** the EPROM and PAL devices  
- 🧠 **Inferring hardware design** from firmware behavior  
- 📚 **Cross-referencing** data from [cpu-ns32k.net](http://www.cpu-ns32k.net/index.html)

Without that resource, this project simply wouldn’t exist.

---

## 🧩 Design Notes

The schematic represents my **best reconstruction** of the intended design, based on the monitor firmware and typical NS32K system architecture.

**Notes:**
- The files here **don’t exactly match** the PCB photo — minor fixes were applied afterward, but I’ve not fabricated a new board.  
- The many **0 Ω jumpers** are deliberate: they simplify debugging and allow trace rerouting without cutting copper. They could be removed in a cleaner revision.

---

## 💾 Hardware (Reconstructed)

```
CPU :  NS32032  @ 10 MHz
FPU :  NS32081  (optional, socketed)
MMU :  NS32082  (optional, untested)
RAM :  512 KB SRAM + 32 KB EPROM
I/O :  2 x 16550 UART-based serial interface + 8255 PIO
ROM :  4 × 2764 EPROMs (TDS monitor)
PALs:  Custom glue logic (reverse-engineered)
BUS :  24-bit address / 32-bit data
```

---

## 🧠 Reflections

Rebuilding this board felt like a mix of **hardware archaeology** and **forensic engineering**.  
Reading EPROMs, decoding PAL logic, and reconstructing timing relationships — all to re-ignite silicon that last saw power in the late ’80s.

Watching the TDS32 monitor prompt appear for the first time in nearly four decades was surreal — a true moment of time travel.

---

## 🖥️ Boot Monitor Output

Here’s the actual terminal output captured from the revived NS32032 system running the **TDS32 Rev 1.00 (28-SEP-87)** firmware:

```
  TDS32    Rev 1.00 28-SEP-87 DEMO KIT  Version

* it

* ccf = 7

* ar

R0  =7220            R1  =700FBC          R2  =F07200          R3  =F0017B      
R4  =207210          R5  =700771          R6  =F07200          R7  =F0017B      

* ac

PC  =0               SB  =9C8101A6        FP  =597210          US  =F0017B      
IS  =8600            SP  =8600            IN  =F07400          PS  =0           
MO  =7220            

* am

MS  =0               EI  =7F7FFFFF        SC  =0               BC  =FFFFFB      
PF0 =FFFFFF          PF1 =0               BP0 =4000000         BP1 =40000000    
PT0 =402000          PT1 =40000           

* af

F0  =0               F1  =200             F2  =820880          F3  =2080000     
F4  =20800022        F5  =1A55A2          F6  =2000020         F7  =FF7FFF7F    
FS  =0               

*
```

> Seeing this prompt again after 37 years confirmed the hardware was alive — the ROM, the bus, and the CPU all working.

---

## 📸 Gallery

![NS32032 PCB](doc/images/PCB_V1_0.jpg)

> *NS32K-Timewarp V1.0 — operational board; schematic files include post-build fixes.*

---

## 🧾 Acknowledgements

Special thanks to:

- 🖥️ **[cpu-ns32k.net](http://www.cpu-ns32k.net/index.html)** —  
  For preserving critical documentation, firmware images, and technical insights.  
- 🧑‍💻 The original **National Semiconductor engineers**, for blazing the trail. 

---

## 📂 Repository Layout

```
schematic/   →  KiCad design files and schematics
board/       →  PCB layout and design notes
eprom/       →  Binary dumps + disassemblies (TBC)
pal/         →  Reverse-engineered PAL equations (TBC)
doc/         →  Images, scans, and reference material
```

---

## 🏁 Current Status

| Component       | Status | Notes |
|-----------------|:------:|-------|
| CPU             | ✅ | Verified operational |
| EPROM firmware  | ✅ | TDS monitor functional |
| PAL logic       | 🚧 | Supplied PAL reverse engineered, to be documented |
| PCB v1.0        | ⚙️ | Works with minor patch wires |
| Documentation   | 🚧 | Further tracing in progress |

---

## 🔮 Future Work

- 🧩 Get a C compiler working and run some code on the board
- 🧩 Write a modern **serial boot monitor** including **HW test features**
- 💾 Expand **I/O** capaboilites 

```
┌───────────────────────────────────────────────┐
│ Built with 1980s silicon, and 2020s time.     │
│                                               │
│ © 2025 NS32K-Timewarp Project                 │
│ https://github.com/drelectro/ns32k-timewarp   │
└───────────────────────────────────────────────┘
```
