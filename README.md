<img src="images/arm.png" height="44">
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<img src="images/inchron-white-531x90.png" height="44">

# Project Callisto

Picking a new SoC and migrating software is a frequent task of OEMs, Tier-1s and 
engineering service providers in cooperation with the silicon manufacturers. With a 
strong focus on the software architecture, INCHRON and Arm teamed up to provide a deep 
understanding of how an application would run on a new SoC, and to anticipate the 
resource consumption.

The solution utilizes trace analysis and model-based simulation. Users will 
significantly lower the risk of choosing the wrong device (picture shows Arm M33 to 
R52 migration example). 


## Use Cases and Challenges

* **Software migration**: Most new systems start with a lot of pre-existing software. 
  The software is refactored and combined with new software. Together it will be 
  deployed to a SoC of choice. New count and types of cores have to be taken into 
  account. Changes in operating systems and communication paths have to be considered. 

* **SoC selection**: By applying the software migration above to different SoCs during 
  the SoC selection process, the SoCs can be compared to each other with regard to 
  the specific software.

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

The library is a central component that stores all relevant parameters that are 
required by each step of the workflow. All vendors of IP, silicon, operating systems, 
BSW, etc. can contribute to the library. The library is used by e.g. Architects at OEMs, 
or T1s who plan the migration to new SoCs: They can focus on their application while
parameters of hardware and operating systems are provided by the library. As the
parameters are often confidential, each project, company, division, or even team can 
have its own version of the library.

## Contribution

This project has been developed by [Arm](https://arm.com) and [INCHRON]
(https://inchron.com). We are looking for potential users as well as for active 
contributors from different areas. If you are interested, please see [Contribution]
(doc/CallForContribution.md).
