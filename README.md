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
* Traces shall contain events for each timing relevant action on target
** Changes of task states (Running, Ready/Preempted, Waiting, Dead)
** Optional: Start/End of Runnable

Classic traces are typically used for "Place-holder for chronVIEW advertisement"

#### Extensions with Additional Performance Data
Classic scheduling traces are extended by additional performance data. In a first step this helps to select representative benchmarks.
Additionally the data is required to consider interference channels in modelling and simulation.
Possible sources for performance data
* DWT counter
* Arm PMU counter
** Clocks
** Instructions
** LD / ST Instructions
** MVE / NEON Instructions
** Cache hit rates
** Cache Refill / WB
** ..
* Proprietary counters 
** AXI manager and subordinate ports
** DRAM controller

#### Trace Processing

##### Identification of OS Overheads

##### Processing of Performance Data

### Extraction of Timing Model
* Tool support for tasks, ?Runnables?, incl. stimulation and net ET
* OS Overhead


### Scaling of Execution Times

#### Categorization

#### Benchmarks

### Mapping to Target Hardware

##### General Approach

##### Consideration of OS Overheads

##### Hypervisors

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