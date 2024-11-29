# Mapping and Simulation

## Model Preparation

After the [model extraction](ModelExtraction.md) from the trace and the
[scaling](Scaling.md) to the intended core types, the application odel is ready to be
analyzed.

## Core and Hypervisor Mapping

During this step, the model elements like isrs and tasks are mapped to instances 
of a specific CoreType. For each mapped CoreType, the model elements need to have a 
CoreSpecificTimeDistribution, which defines the net execution time behavior. Depending 
on the concrete tool chain, a coarse-grained or fine-grain execution time behavior can 
be used.

While it is always possible to map different applications to exclusive subsets of the 
cores in a multicore system on chip, it is also possible to map the application models 
to virtual cores of a hypervisor system, if the tool chain supports this.

## Simulation

When the scaled and mapped application model is simulated, the overhead of the 
operating system must be inserted again, e.g. for context switches. This overhead is 
taken from the OsType description, to which the application was mapped.

With categories similar to the rule set which was is defined by the TracingTool used for 
the model extraction, the OsType defines the net execution time behavior for the 
CoreType, to which the application was mapped. 

Technically, it is possible to use different OsTypes in an application model, e.g. in 
a hypervisor system where different partitions represent different application domains.

The simulation result can be statistically analyzed (e.g. predicted cpu or core load). 
It is also possible to check if timing requirements or event chain requirements are 
fulfilled.
