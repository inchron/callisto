# Scheduling Traces Extended with Performance Data

Classic scheduling traces contain events for each state change of a task or an ISR; sometimes entry/exit events of Runnables/functions are added.
Such traces can be enriched by additional performance data, to extend trace analysis and model based simulation. For later processing events with scheduling information and events with performance data have to be aligned, i.e. that each before/after each scheduling event an event with performance data has to be recorded. Periodic sampling of performance data would require high frequency (which increases trace size/bandwidth) and is more difficult to handle in trace processing.

## Performance Counters 
Almost all processors offer performance counters to count events related to processor performance, e.g. executed instructions, stalls, accesses to different types of memory, cache hits/misses, .... Specification of details is typically part of general architecture specification, but implementation is specific processors is optional and highly configurable.

Modern SoCs offer additional, proprietary counters, e.g. for interconnect transfers and utilization of D-RAM controllers.


### Arm DWT and PMU Counters
Arm v8 Architecture specifies the Data Watchpoint and Trace unit (DWT) and the Performance Monitors Extension (PMU).

## Integration of Performance Data Into Existing Trace Solutions
There a many different ways to generate traces with scheduling events. The most common are observation of variables that contain task states and instrumentation code in hooks provided by the operating system. If observation of variables is used, recording of performance data requires dedicated hardware support. This approach is complex and currently not considered here.
Most operating system offer hooks that are called when tasks, ISRS, ... change their state. In these hooks events are written to trace; here the writing of scheduling events has to be extended by events with performance data.


![Hooks and PMU](images/hooks_pmu.png)


