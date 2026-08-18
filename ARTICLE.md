# From Simulation to Operations: A DCS Infrastructure for Fusion Digital Twins

**By Robert Rainer**  
**August 18, 2026**

Fusion digital twins are often described as high-fidelity models of plasma behavior, magnets, thermal systems, or an entire plant. Those models matter, but a model alone is not an operational digital twin. To become useful across design, commissioning, experiments, maintenance, and optimization, it needs a trustworthy connection to the facility that it represents.

That connection is the distributed control system.

I developed this reference architecture while considering how a modern fusion facility could use an EPICS-centered DCS not only to operate equipment, but also to create the data, timing, configuration, and workflow foundation required for a continuously evolving digital twin. I am now publishing the high-level design as an independent technical concept and an invitation to collaborate.

## The digital twin must share the plant's language

In a large scientific facility, no single application owns the whole machine. Power supplies, vacuum equipment, cryogenics, diagnostics, heating, motion, utilities, timing, machine protection, personnel safety, and data systems all operate at different rates and under different engineering constraints.

The first requirement for a facility-scale twin is therefore not a more complicated model. It is a stable way to identify what the model is observing.

Each important physical quantity needs a governed identity, engineering units, timestamp, quality state, configuration context, and relationship to the equipment hierarchy. EPICS process variables can provide the supervisory namespace and live integration fabric, while a separate configuration and metadata layer records how those signals relate to devices, models, requirements, alarms, and archived data.

This creates a common language between the physical plant and its computational representations.

## A layered controls architecture

The architecture deliberately separates responsibilities.

At the bottom are the physical systems: magnets, power conversion, vacuum, cryogenics, diagnostics, heating and fueling, cooling water, electrical distribution, and facility utilities. Above them are field devices and I/O, followed by PLCs, FPGA or real-time controllers, and independent protection systems where deterministic response is required.

EPICS IOCs and device gateways provide subsystem integration. They normalize protocols, expose health and status, enforce naming conventions, and connect equipment to supervisory services without pretending that Channel Access or PV Access should replace hard real-time control.

Above the control layer are the services that make a digital twin operationally meaningful: timing and event identity, configuration management, archiving, alarms, experiment orchestration, file and metadata services, and controlled data access. Digital-twin applications then consume those governed services for simulation, replay, state estimation, anomaly detection, optimization, and operator assistance.

The operator interface remains at the top—but the architecture is built from the physical process upward.

## One facility, several trust zones

The most important design choice is that the digital twin is not allowed to bypass operational boundaries.

Safety-rated systems and machine protection remain independent authorities. Deterministic control stays close to the equipment. Supervisory commands pass through controlled interfaces. Simulation and optimization services begin read-only and earn broader authority only through verification, validation, access control, and an explicit operating procedure.

This allows powerful modeling and AI/ML tools to participate without making an unvalidated algorithm part of the safety chain.

The same principle applies to networks. Controls, timing, data, management, safety, and external-access functions should be segmented according to risk and operational need. Remote collaboration can be supported through governed gateways and replicated data services rather than direct access to control equipment.

## Time and configuration are part of the model

A digital twin cannot explain an event if it does not know whether two measurements refer to the same instant—or whether the plant configuration changed between them.

The architecture therefore treats timing, event identity, and configuration as first-class services. Facility timing aligns fast data and experimental events. A shared run or event identifier propagates across supervisory records, data files, model executions, and experiment metadata. Configuration snapshots establish which software, calibration, device mapping, model parameters, and operating state were active.

With those foundations, a team can replay a shot or operating sequence, compare predicted and measured behavior, and determine whether the difference came from physics, instrumentation, configuration drift, or control-system behavior.

## A digital twin should grow with the facility

The proposed deployment path is incremental.

### 1. Controls-development twin

Begin with protocol simulators, representative IOCs, operator displays, alarms, and subsystem state machines. This supports controls development before all hardware is available and gives engineers a safe place to test fault handling.

### 2. Virtual commissioning

Connect the simulated plant to production-like controls and sequencing. Test interfaces, naming, timing, permissions, recovery behavior, and operating procedures. Hardware-in-the-loop can be added where it provides the most value.

### 3. Operational mirror

Connect verified read-only services to the facility. Archive synchronized data, capture configuration context, and compare model output with measured behavior. Use the twin for replay, troubleshooting, training, and planning.

### 4. Model-informed operations

After validation, introduce advisory capabilities such as state estimation, anomaly detection, predictive maintenance, and optimization. Any path from advisory output to equipment commands remains controlled, reviewable, and reversible.

This approach avoids the common trap of waiting for a perfect whole-plant model. A useful twin can begin with one subsystem and become more capable as the facility and its models mature.

## Why EPICS is a strong foundation

EPICS already provides many of the patterns needed for long-lived scientific facilities: distributed IOCs, a shared process-variable namespace, alarm and archiving ecosystems, operator interfaces, protocol support, and integration across custom and commercial equipment.

Its role in this architecture is not to do everything. Its value is that it can connect specialized systems without erasing their boundaries. PLCs can remain PLCs. Fast controllers can remain deterministic. Physics services can evolve independently. The DCS provides the supervisory contract through which they are observed, coordinated, and understood.

That makes EPICS particularly well suited to a digital twin that must span both conventional plant systems and experimental physics.

## What I am publishing—and what I am not

I am publishing the architectural structure, engineering rationale, lifecycle, and collaboration model so that the work is visible and can contribute to the fusion-controls conversation.

I am intentionally not publishing a deployable facility package. Exact PV inventories, device and network mappings, credentials, protection settings, detailed interlock logic, procurement estimates, and implementation-specific automation are withheld. Those elements should be developed for a real facility under appropriate technical, safety, cybersecurity, and commercial controls.

This boundary is also practical: a reference architecture becomes valuable through adaptation, validation, commissioning, and lifecycle ownership—not by copying a diagram.

## An invitation to collaborate

I would welcome conversations with fusion companies, national laboratories, universities, and engineering teams interested in developing a controls-connected digital twin.

A collaboration could begin with a small, measurable scope: one vacuum sector, magnet power-supply family, cryogenic loop, diagnostic system, or facility utility. From there, we could establish the namespace, simulator, IOC boundary, timing and configuration context, operator workflow, and validation plan needed to demonstrate the architecture in a real environment.

The goal is not simply to build another visualization. It is to create an operational engineering system that helps a facility design, commission, understand, improve, and safely scale the machine it is building.

If your facility is interested in exploring that path, I am available to help define the architecture and collaborate on a deployment.

**Robert Rainer**  
[rainer1370.com](https://rainer1370.com)  
[github.com/Rainer1370](https://github.com/Rainer1370)  
rainer1370@gmail.com

---

*This article describes an independent reference concept. It is not affiliated with, endorsed by, or a description of the internal systems of Thea Energy or any other fusion company.*
