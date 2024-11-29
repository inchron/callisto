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

1. The existing application is [traced on the old platform](doc/PMUTracing.md).
2. From this trace, a [scheduling and timing model is extracted](doc/ModelExtraction.md).
3. The timing model is [scaled](doc/Scaling.md) for the new platform. The scaling can be
   different for different parts of the application.
4. The application is mapped to the components of the new platform, and then 
   [simulated](doc/MappingAndSimulation.md).
  A report summarizes the predicted behaviour of the application on the new platform.

The basic idea is shown in the picture.

![The workflow](images/workflow.png)

## Library
The library is a central component that stores all relevant parameters that are required by each step of the workflow. All vendors of IP, silicon, operating systems, BSW, ... can contribute to the library. The library is used by Architects at OEMs, T1s, ... who plan the migration to new SoCs: They can focus on their application while parameters of hardware and operating systems are provided by the library. As the parameters are often confidential, each project, company, unit, .. can have its own version of the library.


## Contribution

This project has been developed by [Arm](https://arm.com) and [INCHRON]
(https://inchron.com). We are looking for potential users as well as for active
contributors from different areas. If you are interested, please see [Contribution]
(doc/CallForContribution.md).
