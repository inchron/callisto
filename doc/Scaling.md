# Scaling of Execution Times
Before the extracted application model can be mapped to target SoC, the net execution 
times have to be scaled. The simplest approach is to scale all software elements by 
the same factor. As each algorithm consists of a mix of instructions and the 
dynamically required clocks per instruction depends on processor architectures, 
pipelines, memory architecture,..., a more fine granular scaling is required. Details 
on granularity depend on use case, typical are ISRs, Tasks, Runnables.    

## Categorization
All meta model elements with execution times shall inherit from EClass Categorizable, 
so that their instances can be assigned to Categories.

Categories are defined a libraries and can be used to define the scope of scaling: 
Apply the same scaling factor to each element that is assigned to a Category. The 
categorization can be done based on known functionality (FFT, DCT, StateMachine, ...) 
or based on annotations with performance data that was added during 
[model extraction](ModelExtraction.md).

## Benchmarks
Scaling factors can be derived from benchmarks that are executed on all platforms 
(source and target) and the resulting execution times are stored 
CoreDependedExecutionTimes.

Benchmarks are also assigned to Categories so scaling factors for given categories can 
be easily found in library. 
