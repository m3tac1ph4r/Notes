

### Operating System goals

* Maximum CPU utilization
* Less process starvation
* Higher priority job execution


# Types of Operating System

### Single Process OS :-
Only 1 process executes at a time from the ready queue.
Example: MSDOS


### Batch-Processing OS :-
#important_for_interview 
1. Firstly user prepares his job using puch cards.
2. Then he, submits the job to the computer operator.
3. Operator collects the jobs from different users and sorts the jobs into the batches with similar needs.
4. Then, operator submits the batches to the processor one by one.
5. All the jobs of one batch are executed together.

Disadvantages:
* Priorities cannot be set , if a job comes with some higher priority.
* May lead to starvation (A batch may take more time to complete).
* CPU may become idle in case of I/O operations

![[batch_OS.png]]

Example: ATLAS


### Multi Programming OS :-
#important_for_interview 
Increases CPU utilization by keeping multiple jobs(code and data) in the memory so that the CPU always has one to execute in case some job gets busy with I/O.

1. Single CPU
2. Context switching for processes
3. Swtich happens when current process goes to wait state
4. CPU idle time reduced

Example: THE

### Multi Tasking OS  :-
#important_for_interview 
is a logical extension of multiprograming. We can say it's a 2.0 version of multiprogramming OS.
1. Single CPU
2. Able to run more than one task simultaneously
3. Context swithcing and time sharing used
4. Increases responsivness in the processes which are running
5. CPU idle time is further reduced

> Time sharing means if there are three process P1 , P2 , P3 . P1 is executing. So after some quantum of time P1 will be pause and P2 will start. Same with P2  will pause and P3 will start. Then again P1.
> And if there is any higher priority job then all will stop only higher priority job will run. So time sharing increases the repsonsiveness in the processes.
>
Example: CTSS


### Multi Processing OS :-
#important_for_interview
More than 1 CPU in a single computer.
1. Increases reliability , 1 CPU fails other can work.
2. Better throughput
3. Lesser process starvation (if 1 CPU is working on some process,  other can be executed on another CPU)
Nowdays we use Multi Processing OS in daily life.

Example: Windows

###  Distributed OS :-

1. OS manages many bunches of resources, >=1 CPU, >= 1 memory , >= GPU etc
2. Loosely connected autonomous , interconnected computer nodes.
3. Collection of independent networked communicating and physically seperated computational nodes.

Example: LOCUS, MICROS

### Realtime Operating System :-

1. Real Time error free, computations withing tight-time boundaries.

Example: Airline Traffic Control System , Airlines Reservation System





