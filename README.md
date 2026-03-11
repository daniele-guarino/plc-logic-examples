# plc-logic-examples
PLC control logic examples (Schneider Zelio Soft) with notes on automation and safety
### 📁 ponte-sollevatore/
Complete project for a **hydraulic lifting bridge** control system.

- `Ponte_sollevatore.zm2` — Full PLC logic with commented rungs
- `PG1_Potenza_1.pdf` — Main power circuit (400V AC, protection devices)
- `PG2_Potenza_2.pdf` — Motor power circuit (2.2kW inverter + oil pump)
- `PG3_Ausiliari_1.pdf` — Control circuit (emergency, start/stop, up/down commands)
- `PG4_Ausiliari_2.pdf` — Protective device feedback (differential, thermomagnetic)
- `PG5_IO_PLC.pdf` — PLC I/O mapping

**Key features:**
- Dual-layer safety: hardware emergency contactor (KM1) independent from PLC logic
- Proximity sensor end-stops on both axes (A/B), upper and lower
- Mechanical interlock between UP/DOWN commands
- Thermomagnetic feedback monitoring (400V and 24V circuits)
- Full optical signalling for each operational state

### 📁 azionamenti-motore/
Motor drive control examples demonstrating progressive complexity:
- `Azionamento_Stella_Triangolo.zm2` — Star-delta motor starter with transition timer and mechanical interlock
- `Azionamento_Soft_Starter.zm2` — Soft starter activation sequence with line contactor and switchover delay
- `Marcia_Avanti_e_Indietro.zm2` — Forward/reverse motor control with safety interlock and cycle stop

---

## Technical Notes

- **Software:** Schneider Electric Zelio Soft 2
- **Language:** Ladder Diagram (IEC 61131-3)
- **Safety approach:** Fail-safe principle applied throughout — emergency and stop inputs wired as Normally Closed (NC)
- **All programs** developed for educational and portfolio purposes

---

## Author

**Daniele Guarino**  
ITS Tecnico Superiore in Sistemi Meccatronici — Fondazione ITS Aerospazio/Meccatronica, Torino  
Experience in industrial automation, electrical design and railway safety systems (Alstom — CBTC/SIL4)  
[LinkedIn](https://linkedin.com/in/daniele-guarino-606996201)
