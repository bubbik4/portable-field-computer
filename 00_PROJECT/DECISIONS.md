# Design Decisions Log

This document records important technical and architectural decisions.

---

## DEC-001 - ARM Architecture

Date: 2026-11-06
Status Accepted

### Context

The project requires a compact computing platform suitable for portable use

### Decision

ARM architecture selected as the target platform

### Reasoning

- Compact hardware options.
- Low power consumption potential.
- Availability of SBC platforms.
- Suitable for embedded Linux apps.

### Consequences

The main computing platform must support a suitable Linux distribution and required peripherals.

---

## DEC-002 - Initial Power Source

Date: 2026-11-07
Status: Accepted

### Context

The project requires a portable power solution.

### Decision

Use an external USB-C PD power source during initial prototyping.

### Reasoning

Avoid designing a custom battery pack before system power requirements are known.

### Consequences

A dedicated battery system may be developed during later revision