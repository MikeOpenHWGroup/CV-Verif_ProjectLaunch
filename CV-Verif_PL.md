<!--
Copyright 2026 Eclipse Foundation
SPDX-License-Identifier: Apache-2.0
-->
# Title of Project - "CV Verif"
# Project Launch Proposal
## Date of proposal - 2026-11-24
## Author(s) - Mike Thompson

## Background

Since its inception, a primary activity of the OpenHW Group, now the OpenHW Foundation, has been functional verification of RTL models of RISC-V cores and related components.
It is reasonable to expect that this will continue for many years to come,
although it is also expected that the types of RTL models we verify will expand to non-core 'platform components' such as IOMMU, AIA and NoCs.
The primary vehicle for verification work within OpenHW has been the [core-v-verif](https://github.com/openhwfoundation/core-v-verif) GitHub project.
Originally envisioned as a single platform for the verification of all OpenHW cores,
it is has since evolved into a library of verification components and frameworks for a large variety of OpenHW projects, each using its own independent testbench.

This evolution is seen as either a natural consequence of the success of the platform or a failure of the original platform concept to keep up with the disperate requirements of the OpenHW cores.
It is the opinion of the author that it was the original concept that was flawed and that this has lead us to the current situation,
whereby each OpenHW project that leverages `core-v-verif` does so entirely independently of other projects.
There are many reasons for this:
- While it _is_ possible to create a single verification environment that can meet the needs of all cores,
  it is not practical in the context of an open-source organization with multiple disperate cores in active development.
- Member organizations do not wish to be constrained by the needs of projects not directly tied to the project(s) they rely on and contribute to.
- No single member organization wished to take on the burden of maintaining a large code-base that was not directly applicable to the projects(s) they were part of.

## Proposed Solution

The proposed solution is to create a new Eclipse OpenHW Project to be called `CV-Verif` or `CV-Verification` (which ones sounds better?).
This project will be led by a member of the Eclipse/OpenHW staff and provide the following services to the Membership:
1. Articulation and maintenance of verification processes and methodologies.
2. Maintenance of the **_core-v-verif_** component library.
3. Tools for extracting normative rules from Specifications.
4. Program Management for verification projects.
5. CI regressions for both verification and design IP.
6. An interface to other institutions and organizations providing applicable verification tools and methodologies.
   An example of this is the Archiectural Certification Tests (ACT4) from RISC-V International.

Note that the above is intended to a representative, but not exhaustive list.
From time-to-time the OpenHW TAC may decided to ammend the list of services.
Also, there is no requirement for all, or even any, Eclipse project to use any of the above services.
Each project can select the services that suites its needs.

> [!NOTE]
> While everything in the list above will be free and open-source,
> support for these items and/or activities will be reserved exclusively for Eclipse/OpenHW Members,
> and will be promoted as tangible benefits of being an Eclipse/OpenHW Foundation member.

## High Level Summary of project, project components, and deliverables

The CORE-V Verification project will be a centralized location for all aspects of functional verification of RTL models at the OpenHW Foundation.
The primary components will be the GitHub repositories listed below.
A preliminary set of deliverables is outlined below in the [2027 Timeline](#initial-estimate-of-2027-timeline).

## GitHub Repositories

Currently there are nine OpenHW Foundation GitHub repositories who primary or sole focus is functional verification.
Most, but not all will be transferred from the OpenHW CORE-V project to the OpenHW CV-Verif project.
The Table below details the handling of each of these repositories:

| OpenHW Repository    | Proposed Eclipse Project  | Comments                   |
| -------------------- | ------------------------- | -------------------------- |
| core-v-verif         | OpenHW CV-Verif           | Main repo for Project      |
| cvfpu-uvm            | OpenHW CV-Verif           | Verif Env for CVFPU        |
| core-v-mcu-uvm       | TBD                       | Future OpenHW MCU Project? |
| cv32e20-dv           | OpenHW CV-Verif           | Rename to cve2-dv          |
| cv32e40s-dv          | OpenHW CV-Verif           | To be archived             |
| cv32e40x-dv          | OpenHW CV-Verif           | To be archived             |
| cv32e40p-dv-review   | OpenHW CV-Verif           | Rename to cve4-dv          |
| cv-hpdcache-verif    | TBD                       |                            |
| cvw-arch-verif       | TBD                       | Future OpenHW CVW Project? |

Over the next year, it is expected that verification repositories for CVA6-DCLS, CVA6-Safe, IOMMU, AIA will be launched.
In addition, OpenHW expects to receive a verification repository for CVA6-CHERI.
It is not yet clear which of these, if any, will become part of the CV-Verif project.

## Project license model

The preferred license of the CV-Verif project shall be the [Solderpad 2.1](https://solderpad.org/licenses/) license.
Having said that, any permissive open-source license accepted by the Eclipse Foundation shall also be accepted in this project.
Advice for contributions largely or wholly generated by AI can be found under [Using Artifical Intelligence](https://www.eclipse.org/projects/handbook/#ai) in the Eclipse Project Handbook.

## Summary of market or input requirements

Currently, the verification market in the RISC-V eco-system remains focused on core-level verification.
Over the next few years we can expect to see demand for the following types of designs:
- Safety and Security features (CVA6-Safe, DCLS, CHERI)
- High performance cores (Deep pipelines, multi-threaded)
- Platforms and platform components (IOMMU, AIA, NoC)
- AI-specific ISAs (FP8, FP4, Matrix, Tensor)

### Known market/project requirements at PC gate

Currently, there are three OpenHW projects that use core-v-verif:
1. CVE2: this project is expected to achieve TRL-5 for the CV32E20 configuration in Q4 2026.
   The CVE2 project makes extensive use of **_core-v-verif_**.
2. CVE4: this project is expected to launch in Q1 2027 and is expected to make use of **_core-v-verif_** as a library of VIP.
3. CVA6: the CVA6 uses **_core-v-verif_** as a library of VIP for multiple configurations.

## Who would make use of OpenHW output

Multiple projects either are, or are expected to make direct use of `core-v-verif`:
- CVA6
- CVE2
- CVE4

However, the real growth in adoption will come because `core-v-verif` will be a library of reuseable components,
allowing individual projects to exploit the capabilties of the library, without having to buy-in to any single methodology.
Over time, it is expected that all OpenHW verification efforts will use at least some components of `core-v-verif`.

## Initial Estimate of 2027 Timeline

- Q1 2027: First tagged release of `core-v-verif`.
  - OpenHW hosted CI for at least two CVA6 configurations, one CVE2 configuration and one CVE4 configuration
  - Sail as a Reference Model for at least one configuration of CVE4
  - consolidation and integration of all required features a `RISC-V Toolchain` into a single branch:
  - definition and documentation of a generic "Board Support Package" for RTL testbenches.
  - example testbench.
- Q2 2027: consolidation and integration of all required features of the following UVM VIP into a single branch:
  - Clock and Reset Agents
  - OBI UVM Agent
  - Debug Agent
  - Interrupt Agent
  - Instruction Stream Generator
- Q3 2027: first end-to-end Agentic-AI verification flow for CORE-V cores
  - AI agent control files (e.g. CLAUDE.md)
  - Associated skills for generating DV Plans, coverage models, testbenches and AI-agents
  - Demonstrated coverage closure on a representative core.
- Q4 2027: demonstation plaform for open-source formal verification
  - Architecture-State-Aware Instruction Stream Generator

The above (especially Q1) is rather agressive, but we are not starting "from scratch".
Most of the Q1 and Q2 deliverables already have something in place that is directly applicable to projects such as CVA6, CVE4 and CVE2.
It is proposed that the above estimate be reviewed at least quarterly to the TAC and Cores TG and updated accordingly.

### Release Management

It is proposed to generate a new tagged release at least quarterly.
Release tags shall follow the [symantic versioning](https://semver.org/) format.
This is a departure from the existing release format that ties `core-v-verif` to a specific release of a CORE-V core (e.g. `cv32e40p_v1.8.3`).

Each release will define _what's new in this release_ and will publish features for the following release.

### Potential future enhancements

- [Sail](https://github.com/riscv/sail-riscv) as a reference model for _any_ generic RISC-V core.
- Support for members who wish to use the [ACT4](https://github.com/riscv/riscv-arch-test) certification testsuite.
- A platform for educational out-reach to educational institutions.
- Example formal verification environment for at least one CORE-V cores.

## Explanation of why OpenHW should do this project

Over the past seven years, `core-v-verif` has been in constance use, both by OpenHW members and non-members.
Even as it has evolved to use-case models not originally envisioned, its utility and value to the eco-system as still apparent.
Nevertheless, the lack of centralised oversight has meant that the code-base and the methodology it supports has drifted.
Should we continue on as we are today, the most useful parts of the code-base,
such as the OBI and AXI agents will naturally be absorbed by the projects that most use them,
and opportunities for re-use and shared maintaince will be lost.

### Why should OpenHW _Staff_ do this project

See the second paragraph of the [Background](#background)

## Industry landscape: description of competing, alternative, or related efforts in the industry

Over the past two years, several changes have occured in the Industry that will fundamentally impact how verification of RISC-V cores is done:
- Open-source EDA can now meet the needs of most Industrial users.
- A complete update to the RISC-V International Architectual Certification Test Suite (also known as "ACT4" for historical reasons).
- A significant update to RISC-V International's [Sail](https://github.com/riscv/sail-riscv) Model.
- Capable and cost-effective AI-agents.

These events are interelated.
AI has accelerated the scope and capabilties of both open-source EDA tools and the ACT4 test-suite.
In turn, AI can use these resources to accelerate functional verification of RISC-V cores.
Taken together, the above completely changes the verification landscape for OpenHW.

### Towards an Agentic Verification Flow for OpenHW

The following is a practical AI-driven approach to verification of RISC-V cores that can be executed using technology available today:
1. Generate a DV plan by extracting [normative rules](https://github.com/riscv/docs-resources/blob/main/normative-rules.md) from the Specification.
2. Generate a complete functional coverage model based on the DV plan.
3. Produce a testbench for a RISC-V core using a mix of components from the `core-v-verif` library and components generated by the AI.
4. Run the ACT4 test-suite in the above testbench; identify and fix bugs in both the RTL and Testbench.
5. Produce additional test-programs, as needed to attain full coverage.

While some projects may continue to use `core-v-verif` in traditional ways,
it is the opinion of the author that the primary **_user_** of and contributor to the `core-v-verif` library will be AI-agents working on behalf of OpenHW members.
This will directly impact the goals of the CV-Verif project:
- All stimulus generation must be readily visible to an AI-agent that needs to reason how to use it.
  - test-program running on the core
  - UVM sequences running UVM Agents in the testbench
  - memory mapped capabilties of the testbench (e.g. MTIME)
- A Reference Model must be part of the testbench to determine pass/fail criteria.
- The ACT4 test-suite must be able to run in the same testbench as the AI-agent uses.
- The testbench should be similate correctly using an open-source simulator and reference model to allow the AI to run lots of experiments.

The author is aware that the capabilties of AI will change rapidly and may overtake the above process.

## OpenHW Members/Participants committed to participate

As an Eclipse open-source project, `CV-Verif` will welcome the any members and external contributors who wish to participate.
Participation of member organizations will significantly increase the quality and "buy-in" of the projects outputs.
As such, the Project Lead(s) will endevour to attract direct participation from members.
Having said that, the project is scoped such that it can be executed entirely by the efforts of the Staff.
Member contributions will reduce the technical risk of this proposal and may also allow for an expanded scope or deliverables.
However a lack of contributions will not affect the delivery of this project or the proposed timeline.

## Risks

The single largest risk to CV-Verif is the extent to which AI capabilties expand.
If AI capabilties continue grow at the same pace for the next two years,
it is unlikely that any of the proposed features of the CV-Verif project in this document will be of interest to the community.

## Project Leader(s)

Mike Thompson, Director of Verification at the OpenHW Foundation
The Project Leader shall also assume the role of Project Manager.

### Technical Project Leader(s)

It is desirable to recruit TPLs from the CVE4, CVA6, CVW and SV-Saragantana projects.
