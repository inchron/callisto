# Callisto

The project Callisto targets the prediction of real-time behaviour in very early 
phases of the system design. It was designed to specifically support the migration of 
single core systems to complex systems of chips.

## Workflow

The basic idea is shown in the picture.

![The workflow](images/workflow.png)

1. The existing application is traced on the old platform.
2. From this trace, a scheduling and timing model is extracted.
3. The timing model is scaled for the new platform. The scaling can be different for 
   different parts of the application.
4. The application is mapped to the components of the new platform.
5. A scheduling simulations generates a report, which summarizes the predicted behaviour 
   of the application on the new platform.
