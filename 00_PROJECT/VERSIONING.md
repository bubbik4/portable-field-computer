# Versioning & Revision Control

## 1. Purpose

This document defines the versioning and identification system used throughout the project.

The system is designed to distinguish between project development phases, hardware generations, individual physical units, hardware revisions and software versions.

The primary objective is to maintain clear identification and traceability throughout the entire project lifecycle.

---

## 2. Project Revision System

The project uses the `R` prefix to identify major project generations.

### R0 - Development Phase

`R0` represents the entire development phase preceding the first complete physical prototype.

This phase includes:

- Initial concept development.
    
- Hardware research and component selection.
    
- System architecture design.
    
- Electronics development.
    
- Software development.
    
- Mechanical design and CAD.
    
- Individual subsystem testing.
    
- Preparation for the first complete prototype.
    

All development activities before the first complete prototype belong to R0.

R0 does not represent a completed physical device.

### R1 - First Hardware Generation

`R1` represents the first complete physical hardware generation.

The first physical unit is identified as:

`R1-UNIT-001`

Additional units belonging to the same generation receive sequential identifiers.

Examples:

- `R1-UNIT-001`
    
- `R1-UNIT-002`
    
- `R1-UNIT-003`
    

R1 may include multiple hardware iterations, improvements and modifications without necessarily creating a new project generation.

### R2 - Second Hardware Generation

`R2` represents a major redesign or substantial architectural evolution of the device.

The first physical unit of this generation is identified as:

`R2-UNIT-001`

Subsequent units follow the same numbering convention.

The same principle applies to future generations:

- R3
    
- R4
    
- R5
    

A new generation should only be introduced when significant changes justify a new project revision.

---

## 3. Physical Unit Identification

Every complete physical device receives a unique Unit ID.

### Naming Convention

`R[GENERATION]-UNIT-[NUMBER]`

Examples:

|Identifier|Description|
|---|---|
|R1-UNIT-001|First unit of generation R1|
|R1-UNIT-002|Second unit of generation R1|
|R2-UNIT-001|First unit of generation R2|

Unit identifiers are permanent and must never be reassigned to another physical device.

Individual units may receive hardware modifications without changing their original Unit ID.

Their actual hardware configuration must be documented separately.

---

## 4. Hardware Revision System

Hardware components and custom-designed assemblies use independent revision identifiers.

### Naming Convention

`REV [LETTER]`

Examples:

- Rev A - Initial design.
    
- Rev B - Modified design.
    
- Rev C - Further design iteration.
    
- Rev D - Subsequent revision.
    

Hardware revisions are independent of the overall project generation.

### Example Component Identifiers

|Component|Identifier|
|---|---|
|Main PCB|PCB-MAIN Rev A|
|Power PCB|PCB-PWR Rev B|
|Enclosure|CASE Rev A|
|Display Assembly|DISPLAY Rev A|
|Control Board|PCB-CTRL Rev A|

A hardware revision must be updated when a meaningful design change is introduced.

Minor documentation corrections do not automatically require a new hardware revision.

---

## 5. Software Versioning

Software developed specifically for the project uses Semantic Versioning.

### Naming Convention

`MAJOR.MINOR.PATCH`

Examples:

- v0.1.0
    
- v0.2.0
    
- v0.2.1
    
- v1.0.0
    
- v1.1.0
    

### Version Rules

**MAJOR**

Introduces incompatible changes or a substantial architectural redesign.

**MINOR**

Introduces new functionality while maintaining compatibility.

**PATCH**

Introduces bug fixes, minor corrections and non-breaking improvements.

Software components are versioned independently.

Examples:

- ESP32 Firmware: v0.1.0
    
- System Dashboard: v0.2.0
    
- Auxiliary Control Software: v1.0.0
    

Third-party software retains its original upstream version numbers.

---

## 6. Git Version Control

Git is used to track changes across the entire project repository.

### Commit Naming

Commits should use short, descriptive English messages.

Examples:

- Initial project structure
    
- Add SBC research
    
- Update power architecture
    
- Document display interface
    
- Add enclosure prototype
    
- Fix ESP32 firmware configuration
    

### Git Tags

Git tags may be used to mark important project milestones and stable configurations.

Examples:

- `r0-development`
    
- `r0-prototype-ready`
    
- `r1-unit-001`
    
- `r1.1-development`
    

Tags identify specific repository states and do not replace physical Unit IDs or hardware revisions.

---

## 7. Development Milestones

The following milestones define important project lifecycle stages.

|Milestone|Description|
|---|---|
|R0-DEV|Initial development|
|R0-RESEARCH|Research and component selection|
|R0-DESIGN|Architecture and mechanical design|
|R0-PROTOTYPE-READY|Ready for first complete assembly|
|R1-UNIT-001|First physical prototype|
|R1-TESTED|First generation tested|
|R1-OPERATIONAL|First generation operational|
|R2-UNIT-001|First unit of the second generation|

Milestones are identifiers for project progress, not separate hardware revisions.

---

## 8. Revision Management Rules

1. Project generations are independent of individual hardware revisions.
    
2. Physical Unit IDs are permanent and unique.
    
3. Hardware components maintain their own revision history.
    
4. Software components use Semantic Versioning.
    
5. Git commits track all meaningful repository changes.
    
6. Git tags identify important development milestones.
    
7. A new project generation requires a significant architectural or functional change.
    
8. All hardware modifications affecting a physical unit should be documented.
    
9. Historical configurations must remain traceable.
    

---

## 9. Current Project Version

|Property|Current Value|
|---|---|
|Project Revision|R0|
|Development Phase|Initial Development|
|First Hardware Generation|R1|
|First Physical Unit|R1-UNIT-001|
|Hardware Revision|Not yet assigned|
|Software Version|Not yet assigned|

---

## 10. Document Maintenance

This document defines the official project versioning convention.

Changes to the versioning system should be documented and committed to the repository.

All project documentation should follow the conventions established here.