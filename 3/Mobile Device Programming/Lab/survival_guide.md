# ย้ายไปที่ [http://itkmitl10.github.io/mobile%20device%20programming/2014/08/26/mdp-survival-guide/]

# Survival Guide

- วิธีทำให้ Android Emulator ทำงานเร็วขึ้น
  1. ลง Intel x86 Atom System Image ใน Android API ที่ต้องการ
  2. ลง Inter x86 Emulator Accelerator (HAXM installer) ใน Extras
  3. เลือก CPU/ABI ของ Android Emulator ที่ต้องการเป็น Intel Atom (x86)
  4. ติก Use Host GPU ใน Emulation Options
- วิธีแก้ปัญหาเบื้องต้น
  - ตรวจสอบ SDK ที่จำเป็น
    - SDK Platform สำหรับเวอร์ชั่นที่ต้องการ
    - ARM EABI v7a System Image (ถ้าต้องการสร้าง Emulator เวอร์ชั่นนั้น)
  - หลังลง SDK เสร็จแล้วควรปิดแล้วเปิด Eclipse ใหม่
  - ตรวจสอบการ Link โปรเจค (ในบางกรณี)
  - คลิกขวาที่โปรเจคแล้วคลิก "Refresh"
  - เลือกเมนู "Project" คลิก "Clean"
  - ปิดแล้วเปิด Eclipse ใหม่
  - ลบโปรเจคแล้วสร้างใหม่
