# Callisto

The project Callisto targets the prediction of real-time behaviour in very early 
phases of the system design. It was designed to specifically support the migration of 
single core systems to complex systems of chips. Changes in the underlying processor architectures are also supported.

## Use Cases and Challenges

### Migration Without Hypervisor
* 1 Old Core ==> 1 New Core

### Migration With Hypervisor
* n Old Cores ==> m New Cores
* Hypervisor with TDMA

### Scaling of Execution Times and Other Effects
* One scaling factor is not sufficient
* Goal: Fine granular scaling of execution times (Tasks, Runnables)
* Additional consideration of interference channels, if software is executed in parallel on multiple cores

## Workflow

* Somewhere we have to explain the library based approach.
* Library is prepared by Arm, SIP, OSVendor
* Library is used when Architect at OEM, T1, ... plans migration to new SoC

The basic idea is shown in the picture.

![The workflow](images/workflow.png)

### Tracing of Source System

#### Classic Scheduling Traces

#### Extensions with Additional Performance Data
* Arm PMU
* Proprietary counters e.g. on AXI and DRAM controller

### Extraction of Timing Model


### Scaling of Exeuction Times

### Mapping to Target Hardware

### Model Based Timing Simulation and Report Generation

Original description from first version, shall be replaced by above sections
1. The existing application is traced on the old platform.
2. From this trace, a scheduling and timing model is extracted.
3. The timing model is scaled for the new platform. The scaling can be different for 
   different parts of the application.
4. The application is mapped to the components of the new platform.
5. A scheduling simulations generates a report, which summarizes the predicted behaviour 
   of the application on the new platform.


### Case Study
WP7 or artificial example