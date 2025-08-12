# CPU Boot Process — From Power-On to OS Loading

## 1. Power-On & CPU Reset
- **Power button pressed** → Power supply (PSU) stabilizes voltage.
- **CPU reset signal** is triggered:
  - Registers cleared to default values.
  - Program Counter (PC) set to a **fixed reset vector address** (e.g., `0xFFFF0` for x86).
- This fixed address is **hard-wired** to point to the BIOS firmware chip.

---

## 2. BIOS Execution from ROM/Flash
- **BIOS (Basic Input/Output System)** is stored in **non-volatile memory**:
  - ROM (Read-Only Memory)
  - EEPROM (Electrically Erasable Programmable ROM)
  - Flash Memory
- CPU **fetches instructions directly from BIOS chip** — no RAM is involved yet.
- Early BIOS code is small and designed to run directly from ROM.

---

## 3. POST (Power-On Self Test)
- BIOS begins **hardware initialization**:
  - Checks CPU registers & flags.
  - Initializes and tests RAM.
  - Detects and initializes GPU, storage controllers, keyboard, etc.
- If errors occur (e.g., bad RAM), BIOS emits **beep codes** or shows error messages.

---

## 4. RAM Initialization
- Once RAM passes the POST check, the BIOS can:
  - Use RAM for temporary storage.
  - **Shadow** some BIOS code from ROM into RAM for **faster execution** (RAM is much faster than ROM).

---

## 5. Boot Device Selection
- BIOS checks **boot order** (from CMOS settings):
  1. USB drive
  2. SSD/HDD
  3. Network (PXE boot)
- Locates a valid **boot sector** or bootloader.

---

## 6. Bootloader Loading
- BIOS reads the **first 512 bytes** (MBR — Master Boot Record) or UEFI bootloader from the selected device **into RAM**.
- Execution control is passed to the **bootloader**.

---

## 7. OS Loading
- Bootloader loads the operating system kernel into RAM.
- Initializes kernel subsystems.
- Passes control to the OS, which takes over the system.

---

### Summary Flow
1. **Power On**
2. **CPU Reset** → PC points to BIOS address
3. **BIOS runs from ROM**
4. **POST checks hardware**
5. **RAM initialized**
6. **BIOS copies parts to RAM (shadowing)**
7. **Boot device selected**
8. **Bootloader loaded into RAM**
9. **OS loaded into RAM**
10. **OS takes control**

---

### Key Notes
- BIOS/UEFI firmware **starts directly from ROM/flash**, not RAM.
- **Shadowing** into RAM happens **after** RAM is initialized for speed.
- Modern systems often use **UEFI** instead of traditional BIOS, but the core steps are similar.
