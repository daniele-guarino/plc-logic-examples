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
- 

**Key features:**
- Dual-layer safety: hardware emergency contactor (KM1) independent from PLC logic
- Proximity sensor end-stops on both axes (A/B), upper and lower
- Mechanical interlock between UP/DOWN commands
- Thermomagnetic feedback monitoring (400V and 24V circuits)
- Full optical signalling for each operational state

  ## Ponte Sollevatore — Functional Description

stateDiagram-v2
    [*] --> FERMO : Power ON

    FERMO --> ABILITATO : KA1=0 AND KA8=0 AND KA9=0 AND KA10=0
    ABILITATO --> FERMO : KA1=1 OR KA8=1 OR KA9=1 OR KA10=1
    ABILITATO --> ALIMENTATO : KA2=1
    ALIMENTATO --> ABILITATO : KA2=0
    ALIMENTATO --> SALITA : KA3=1 AND FC_Sup_A=0 AND FC_Sup_B=0
    SALITA --> ALIMENTATO : FC_Superiore_A=1 OR FC_Superiore_B=1
    ALIMENTATO --> DISCESA : KA4=1 AND FC_Inf_A=0 AND FC_Inf_B=0
    DISCESA --> ALIMENTATO : FC_Inferiore_A=1 OR FC_Inferiore_B=1
    SALITA --> FERMO : KA1=1 OR KA8=1 OR KA9=1 OR KA10=1
    DISCESA --> FERMO : KA1=1 OR KA8=1 OR KA9=1 OR KA10=1

### Functional Logic Description (EN)

1. System at rest — all outputs de-energised.
2. If KA1=0 AND KA8=0 AND KA9=0 AND KA10=0 → system enabled, HL1=OFF.
3. If KA2=1 → system powered, HL2=ON.
4. If KA3=1 → UP command active, HL3=ON, KA4 interlocked (=0).
5. If UP command active → KA5=1, KA7=1, KA6=0.
6. If KA4=1 → DOWN command active, HL4=ON, KA3 interlocked (=0).
7. If DOWN command active → KA6=1, KA7=1, KA5=0.
8. If Upper end-stop A or B=1 → UP command deactivated.
9. If Lower end-stop A or B=1 → DOWN command deactivated.
10. If KA1=1 OR KA8=1 OR KA9=1 OR KA10=1 → system stopped, HL1=ON.

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
