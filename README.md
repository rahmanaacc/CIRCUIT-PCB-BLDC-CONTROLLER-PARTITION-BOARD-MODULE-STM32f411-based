# Modular BLDC Motor Controller Partition Board (STM32F411CEU6 Based)

Projek Capstone ini berfokus pada perancangan hardware modul *controller* motor BLDC (Brushless DC) berbasis mikrokontroler **STM32F411CEU6** menggunakan metode kontrol **6-step commutation (trapezoidal control)**. 

Arsitektur hardware dirancang secara modular (*partition board*) dengan memisahkan domain sinyal kendali, *gate driver*, dan tingkat daya (*inverter stage*). Pemisahan topologi ini bertujuan untuk meminimalkan *noise* switching (EMI), mengoptimalkan manajemen termal, serta mempermudah proses pengujian dan *troubleshooting* secara independen pada tiap modul.

---

## Modul Hardware Utama

Repository ini terdiri dari tiga modul papan terpisah (*partition boards*):

1. **Control-MCU Module (`Control-MCU With Voltage Drop Detector 0,5mm`)**
   * Modul pemroses utama berbasis mikrokontroler **STM32F411CEU6**.
   * Dilengkapi rangkaian *Voltage Drop Detector* dengan lebar jalur *trace* teroptimasi 0,5 mm untuk menjaga integritas sinyal dan stabilitas tegangan referensi MCU.
   * Berfungsi mengolah algoritma **6-step commutation**, membaca sinyal *feedback* posisi rotor, dan menghasilkan sinyal PWM transmisi ke *gate driver*.

2. **Driver & Switching Optimization Circuit (`DRIVER and SWITCHING OPTIMIZATION CIRCUIT REV 2`)**
   * Modul perantara *gate driver* yang mengisolasi sinyal logika kendali level rendah dari tegangan tinggi *inverter*.
   * Mengintegrasikan rangkaian optimasi *switching* untuk mempercepat *rise/fall time* MOSFET, mengurangi *switching loss*, dan mencegah kondisi *cross-conduction* (*shoot-through*).

3. **Inverter Circuit (`INVERTER CIRCUIT REV 2 FIX`)**
   * Modul tingkat daya (*power stage*) berupa jembatan tiga fasa (*three-phase bridge inverter*).
   * Didesain untuk menangani arus tinggi dengan penataan jalur *copper pour* teroptimasi dan konektivitas daya fasa motor yang andal.

---

## Struktur Repository

```text
CIRCUIT-PCB-BLDC-CONTROLLER-PARTITION-BOARD-MODULE-STM32f411-based/
│
├── Control-MCU With Voltage Drop Detector 0,5mm/
│   ├── Control-MCU.kicad_sch          # Skematik KiCad Modul MCU
│   ├── Control-MCU.kicad_pcb          # Layout PCB Modul MCU
│   └── Control-MCU.kicad_pro          # Berkas Proyek KiCad Modul MCU
│
├── DRIVER and SWITCHING OPTIMIZATION CIRCUIT REV 2/
│   ├── DRIVER and SWITCHING OPTIMIZATION CIRCUIT.kicad_sch
│   ├── DRIVER and SWITCHING OPTIMIZATION CIRCUIT.kicad_pcb
│   └── DRIVER and SWITCHING OPTIMIZATION CIRCUIT.kicad_pro
│
├── INVERTER CIRCUIT REV 2 FIX/
│   ├── INVERTER CIRCUIT REV 2 FIX.kicad_sch
│   ├── INVERTER CIRCUIT REV 2 FIX.kicad_pcb
│   └── INVERTER CIRCUIT REV 2 FIX.kicad_pro
│
└── README.md
