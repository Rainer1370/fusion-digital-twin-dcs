# Architecture Overview

## Design objective

Create a controls infrastructure that supports facility operation and a progressively higher-fidelity digital twin without allowing simulation, analytics, or optimization services to bypass deterministic control, machine protection, personnel safety, or cybersecurity boundaries.

## Functional layers

| Layer | Responsibility | Typical technologies |
|---|---|---|
| Operator and engineering workflows | Operations, alarms, trends, procedures, engineering access | Phoebus, web tools, notebooks |
| Twin and optimization services | Simulation, replay, state estimation, advisory optimization | Physics codes, Python/C++, ML services |
| Data and context services | Archiving, metadata, configuration, run identity, files | Archiver, databases, object/file storage |
| Supervisory integration | Shared namespace, subsystem state, commands, health | EPICS IOCs, Channel Access, PV Access |
| Deterministic control and protection | Fast loops, sequencing, permissives, interlocks | PLCs, FPGA/RT controllers, safety systems |
| Device and I/O | Protocols, sensors, actuators, signal conditioning | Industrial networks, DAQ, field I/O |
| Physical plant | Fusion experiment and supporting plant | Magnets, vacuum, cryogenics, diagnostics, utilities |

## Cross-cutting services

- Facility timing and synchronized timestamps
- Run, shot, sequence, and event identity
- Configuration and calibration provenance
- Authentication, authorization, and audit trails
- Alarm philosophy and state aggregation
- Software deployment, health monitoring, and recovery
- Requirements traceability and interface governance

## Authority model

The twin begins as a read-only consumer. Advisory outputs are reviewed by operators or engineering workflows. Any later closed-loop use requires facility-specific validation, bounded authority, safe fallback behavior, cybersecurity review, and independent protection that does not depend on the twin.

## Deployment pattern

1. Model the equipment hierarchy and interface contracts.
2. Build simulators and representative IOCs.
3. Validate displays, alarms, sequencing, and failure behavior.
4. Introduce hardware-in-the-loop where risk or value warrants it.
5. Connect read-only operational data with timing and configuration context.
6. Add replay, model comparison, diagnostics, and advisory services.
7. Expand only after verification and operational acceptance.

## Facility-specific work intentionally excluded

This public overview is not a safety basis or detailed design. A real deployment requires equipment lists, network and cybersecurity design, hazard analysis, protection requirements, timing budgets, data-rate sizing, availability targets, configuration management, commissioning procedures, and formal verification appropriate to the facility.
