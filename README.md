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

### Impact of New Target Hardware on Software Architecture
* Depending on integration scenario software architecure has to be adapeted for target system
  * Mapping of software componentes to clusters and cores
  * Consideration of reconfiguration or exchange of BSW stack ==> Changed structure of tasks and mainfunctions
   

### Scaling of Execution Times and Other Effects
* One scaling factor is not sufficient
* Goal: Fine granular scaling of execution times (Tasks, Runnables)
* Additional consideration of interference (channels), if software is executed in parallel on multiple cores

## Workflow

1. The existing application is traced on the old platform.
2. From this trace, a scheduling and timing model is extracted.
3. The timing model is scaled for the new platform. The scaling can be different for different parts of the application.
4. The application is mapped to the components of the new platform.
5. A scheduling simulations generates a report, which summarizes the predicted behaviour of the application on the new platform.

The basic idea is shown in the picture.

![The workflow](images/workflow.png)

* Somewhere we have to explain the library based approach.
* Library is prepared by Arm, SIP, OSVendor
* Library is used when Architect at OEM, T1, ... plans migration to new SoC


### Tracing of Source System

#### Classic Scheduling Traces
* Traces shall contain events for each timing relevant action on target
  * Changes of task states (Running, Ready/Preempted, Waiting, Dead)
  * Optional: Start/End of Runnable

Classic traces are typically used for "Place-holder for chronVIEW advertisement"

#### Extensions with Additional Performance Data
Classic scheduling traces are extended by additional performance data. In a first step this helps to select representative benchmarks.
Additionally the data is required to consider interference channels in modelling and simulation.
Possible sources for performance data
* DWT counter
* Arm PMU counter
 * Clocks
 * Instructions
 * LD / ST Instructions
 * MVE / NEON Instructions
 * Cache hit rates
 * Cache Refill / WB
 * ..
* Proprietary counters 
 * AXI manager and subordinate ports
 * DRAM controller

#### Trace Processing
Traces captured from target contain raw data that needs further processing.

##### Identification of OS Overheads
* Overhead for context switches is often not directly visible in trace
* In which form overhead is included in other elements (tasks, idle task), depends on trace tool (-chain).
* Trace post processing required
 * Insert overhead in dedicated overhead tasks
 * Remove overhead from other elements
 * Specification of details in library
 
##### Processing of Performance Data
* Traces contain raw data only
 * Monotonic counters with overflow
 * 
Task processing to generated required data
* Combine counters e.g. clock and instruction counter to CPI 
* Assign differences in counters to tasks, runnables, ... (similar to net ET)

### Extraction of Timing Model
* Tool support for tasks, ?Runnables?, incl. stimulation and net ET
* Remove/replace OS Overhead

### Integration of Additional Data Sources
--- Optional section---
If additional data is available this can be added to the model. 
Typical data sources
* AUTOSAR CP SystemDescription
* AUTOSAR CP ECU Configuration (OsConfiguration, RTE Configuration)
* Proprietary data bases e.g. for signals exchanged between components

### Scaling of Execution Times
* Predict net execution times on target SoC
* Granularity depends on use case. Typical task, runnable level,...
* 
How to find scaling factors?

#### Categorization
* Categories in library
* Used to define scope of scaling
* Can be assigned based on known functionality (FFT, DCT, StateMachine, ...)
* Annotations
  * Performance data
  * Can be filled from processed traces

#### Benchmarks
* Benchmarks are executed on all platforms
* Results are stored in CoreDependedExecutionTimes 
* Scaling factors between platforms can be derived
* Linked to categories
* Helps to find representative categories


### Mapping to Target Hardware

##### General Approach
* Models that were extracted from traces can be simulated with the same hardware on which the trace was recorded. This allows detailed analysis or the source system in high load situations, corner cases, ....
* To analyse the behaviour on target hardware the software from source system has to be mapped on target hardware.

##### Consideration of OS Overheads
* The OS overheads (context switch, ISR entry/exit, ...) are very different on target hardware. The overheads were on source hardware were identified during trace processing and can be removed easily. The overheads on target hardware are part of library and can be applied according to new mapping.

##### Hypervisors

### Model Based Timing Simulation and Report Generation


### Case Study
WP7 based on ST(Italy) input  or artificial example
Big version: ST(Munich) PPC==>Arm



# Old Stuff to Be Deleted
Original description from first version, shall be replaced by above sections
1. The existing application is traced on the old platform.
2. From this trace, a scheduling and timing model is extracted.
3. The timing model is scaled for the new platform. The scaling can be different for 
   different parts of the application.
4. The application is mapped to the components of the new platform.
5. A scheduling simulations generates a report, which summarizes the predicted behaviour 
   of the application on the new platform.
