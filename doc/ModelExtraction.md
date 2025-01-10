# Model Extraction

Traces, that have been [recorded from an application](PMUTracing.md) running on the old 
platform, contain raw data that needs further processing:

* The OS overhead is included in the trace and must be separated from the application.
* The model and its timing behaviour can be extracted from the trace.
* Performance counters indicate characteristic details of the application and  
  annotate the model elements.
* Finally, additional information can be added manually to the model.

## Tracing Tool Configuration

The EClass TracingTool from the callisto.ecore aggregates the details and specific 
values to differentiate application behavior from tracing tool limitations and operating 
system behavior. In a classic trace analysis the overhead around the context switch 
between two tasks has to be considered in response time and load analysis. However, 
when the application model is extracted, and the behavior is extrapolated to a 
different operating system, the overhead must not be considered.

The TracingTool refers to a combination of a CoreType and an OsType to which it 
applies, and contains a glitch threshold, a set of overhead extraction rules, and 
defines operations on recorded performance counter values.

### Scheduling Glitches

The Glitch Threshold defines the length of a scheduling glitch, which can often be 
seen after an interrupt which triggers a context switch. When the implementation of 
the OS switches to a new task during the return from the interrupt, many tracing tools 
records this as a sequence of exit interrupt, execute old task, switch to new task.

During the execution of the old task, no code or functionality of the old task is 
executed, instead operating system code is executed before the switch to the new task 
is signaled (or recognized) by the tracing tool. To differentiate situations where the 
interrupt triggers the context switch from those where the application executed after 
the interrupt triggers the context switch (e.g. blocking on a semaphore), the glitch 
threshold is used as a heuristic.

### Overhead Extraction Rules

The tracing tool identifies a certain set of extraction rules by name (this must 
correspond to an implementation in an analysis tool). Specific parameters for rules 
can be added.

> We are actively looking for other tool vendors to improve the formalization of 
> extraction rules. Please see [Call For Contribution](CallForContribution.md).

Currently, extraction rules exist for the overhead of (plain) interrupts, category 1 and 
category 2 interrupts, context switches, switches and reconfiguration of memory 
processing units, handling of secure tasks, and switches between virtual cores in a 
hypervisor environment. The list is defined by the enumeration OverheadType.

Each extraction rule uses two parameters to subtract the overhead from the recorded 
application timing: The overhead time and a ratio. The overhead is the time, which is 
subtracted from the one or both tasks to which a rule applies, while the ratio defines 
how much of the overhead is subtracted from the task e.g. left of a context switch, 
and how much from the task right of that point.  


## Extraction of Timing Model

After the identification of the operating system overhead, the application model can 
be extracted from the trace. The level of detail depends not only on the events 
recorded by the tracing tool, but also on the capabilities of the modelling and 
simulation tools, which are used later.

In general, the following details should be extracted from the trace:

* Interrupts, their net execution time behavior and their activation pattern;
* Tasks, their net execution time behavior and their activation pattern;
* Functions, their net execution time behavior and the behavior of their callers 
  (which may be tasks or other functions);


## Extraction of Performance Data

The tracing tool also evaluates the performance counters in the trace, calculates the 
advance of free-running counters between two consecutive samples, and assigns the 
reading to respective isr, task or function. Additionally, the callisto.ecore defines 
a simple means to express calculations, i.e. to calculate the ratio of load/store 
instruction and the number of total instructions.

Such derived values can either be added to the extracted model, where they are used to 
assist the [categorization of model elements](Scaling.md), or inserted into the trace, 
where they can be shown during a trace analysis.


## Integration of Additional Data Sources

Depending on the concrete tool chain, the extracted model can be enriched by other 
data sources, e.g. AUTOSAR extracts, to refine the behavior and yield better results. 
A very common use case is the refinement of the recorded activation times (which may 
jitter and drift) with an ideal timing (according to a specification).
