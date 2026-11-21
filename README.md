<div align="center">

# 🔌 PROVEtech:RE FMU Importer

**FMI 1.0 · 2.0 · 3.0  |  Co-Simulation · Model Exchange · Scheduled Execution  |  FMI-LS-BUS**

*A high-level overview of the FMU examples used to validate the PROVEtech:RE FMU importer.*

</div>

---

## 📑 Contents

1. [Importer capabilities](#-1-importer-capabilities)
2. [FMU examples and exporters](#-2-fmu-examples-and-exporters)
3. [Compatibility summary](#-3-compatibility-summary)

---

## ⚙️ 1. Importer capabilities

| Area | Support in PROVEtech:RE |
|:-----|:------------------------|
| 🧩 **FMI versions** | 1.0, 2.0, 3.0 |
| 🔁 **Interface types** | Co-Simulation (CS), Model Exchange (ME), Scheduled Execution (SE, FMI 3.0 only) |
| ⏱️ **FMI 3.0 features** | Clocks (periodic, triggered, countdown), Event Mode, structural parameters |
| 🚌 **FMI-LS-BUS** | Network Abstraction (Low-Cut) for CAN, LIN, FlexRay and Ethernet<br>Physical Signal Abstraction (High-Cut) for CAN |
| 🔗 **Bus coupling** | Internal relay (ideal or timed), Bus Simulation FMU, direct connection, external data-carrying CAN port |
| 🔍 **Observation** | LS-BUS terminals are disassembled onto PROVEtech:RE virtual-device ports (CAN, LIN, FlexRay, Ethernet/generic) |
| 💻 **Platforms** | Windows 10/11 x86-64<br>Ubuntu 22.04/24.04 x86-64 and arm64 |

> **Legend:** **CS** = Co-Simulation · **ME** = Model Exchange · **SE** = Scheduled Execution

---

## 📦 2. FMU examples and exporters

| Family / folder | FMUs | Exporter (`generationTool`) | FMI | Interfaces | Bus / feature |
|-----------------|------|-----------------------------|-----|------------|---------------|
| Modelica Reference FMUs (`referencefmus/fmi1`) | BouncingBall, Dahlquist, Feedthrough, Resource¹, Stair, VanDerPol | Reference FMUs (development build) | 1.0 | Separate CS and ME FMUs | Plain signals, state events |
| Modelica Reference FMUs (`referencefmus/fmi2`) | BouncingBall, Dahlquist, Feedthrough, Resource, Stair, VanDerPol | Reference FMUs (development build) | 2.0 | CS + ME | Plain signals |
| OpenModelica (`referencefmus/fmi2`) | AdaptiveCruise | OpenModelica Compiler v1.26.3 (64-bit) | 2.0 | ME | Plain signals |
| Modelica Reference FMUs (`referencefmus/fmi3`) | BouncingBall, Dahlquist, Feedthrough, Resource, Stair, StateSpace, VanDerPol | Reference FMUs (development build) | 3.0 | CS + ME | Plain signals, arrays |
| Modelica Reference FMUs (`referencefmus/fmi3`) | Clocks | Reference FMUs (development build) | 3.0 | SE | Clocks / model partitions |
| FMI-LS-BUS demo FMUs (`fmus/`) | DemoCanNodeTriggeredOutput, DemoCanBusSimulation, DemoFlexRayNode1/2, DemoFlexRayBusSimulation, DemoLinCommander, DemoLinResponder, DemoLinResponderSilent | *not declared* ² | 3.0 | CS | CAN, FlexRay, LIN Low-Cut; CAN and FlexRay Bus Simulation FMUs |
| dSPACE V-ECUs (CAN) | DspaceController / DspaceEngineModel (Triggered, Countdown) | SystemDesk V-ECU Generation Framework 25.1.0.3265245 | 3.0 | CS | CAN Low-Cut, triggered and countdown clocks, embedded XCP-on-TCP |
| dSPACE V-ECUs (FlexRay) | DspaceFlexrayController, DspaceFlexrayEngineModel | SystemDesk V-ECU Generation Framework 25.1.0.2844342 | 3.0 | CS | FlexRay Low-Cut, embedded XCP-on-TCP |
| dSPACE V-ECUs (Ethernet) | Transmitter, Receiver | SystemDesk V-ECU Generation Framework 25.1.0.3319226 | 3.0 | CS | Ethernet Low-Cut |
| dSPACE CAN-LIN (`dspace/CAN-LIN`) | Controller, EngineModel, Combi | SystemDesk V-ECU Generation Framework 26.1.0.3761436 | 3.0 | CS | CAN + LIN Low-Cut, multi-terminal ECU, embedded XCP-on-TCP |
| dSPACE Ethernet (`dspace/Ethernet`) | TcpClient, TcpServer | SystemDesk V-ECU Generation Framework 25.1.0.3545527 | 3.0 | CS | Ethernet Low-Cut (TCP), embedded XCP-on-TCP |
| PMSF (`fmus/`) | ECU30Base, TCU30Base | PMSF Manual FMU Framework | 3.0 | CS | CAN High-Cut (powertrain signals) |
| Synopsis – Low-Cut | DemoCanNode* (8 variants), DemoEthernetNodeLowCut | *not declared* ² | 3.0 | CS | CAN (1–4 buses, triggered, periodic, parametrized), Ethernet |
| Synopsis – LIN | DemoLinNodeCoordinatorScheduled, DemoLinNodeResponderTriggeredOutput | Silver LinLsBus Test FMUs | 3.0 | CS | LIN Low-Cut |
| Synopsis – High-Cut | DemoCanNodeHighCutEngine, DemoCanNodeHighCutAllTypes | DBC2FMI Converter v1.0 | 3.0 | CS | CAN High-Cut (PSA) |
| Synopsis – High-Cut | DemoCanNodeHighCutMultiplexed, DemoCanNodeHighCutLoadedBus | Manual | 3.0 | CS + ME | CAN High-Cut (multiplexed, loaded bus) |
| Akkodis (`Akkodis`) | SomeIpNode | lsbus_extensions demos | 3.0 | CS | Ethernet Low-Cut, SOME/IP + SOME/IP-SD |

> ¹ Resource is available only as a CS FMU for FMI 1.0.<br>
> ² The Modelica Association Project FMI Demo FMUs.

---

## ✅ 3. Compatibility summary

| Exporter | FMI | Interfaces | Low-Cut | High-Cut | Bus FMU | Status |
|:---------|:---:|:----------:|:--------|:---------|:--------|:-------|
| **Modelica Reference FMUs** / hand-written | 1.0, 2.0, 3.0 | CS, ME, SE | – | – | – | ✅ Covered (full matrix) |
| **OpenModelica** 1.26.3 | 2.0 | ME | – | – | – | ✅ Covered (smoke test) |
| **FMI-LS-BUS demo FMUs** | 3.0 | CS | CAN, LIN, FlexRay | – | CAN, FlexRay | ✅ Covered |
| **dSPACE** SystemDesk 25.1 | 3.0 | CS | CAN, FlexRay, Ethernet | – | Uses the demo Bus FMU | ✅ Covered |
| **dSPACE** SystemDesk 25.1 / 26.1 (CAN-LIN, TCP) | 3.0 | CS | CAN, LIN, Ethernet | – | – | ✅ Covered |
| **PMSF** Manual FMU Framework | 3.0 | CS | – | CAN | – | ✅ Covered |
| **Synopsis** (Silver / DBC2FMI / manual) | 3.0 | CS, ME | CAN, LIN, Ethernet | CAN | – | ✅ Covered<br> |
| **Akkodis** lsbus_extensions | 3.0 | CS | Ethernet (SOME/IP) | – | – | ✅ Covered |

