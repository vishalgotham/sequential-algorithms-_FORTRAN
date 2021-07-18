# MPI-Fortran
A sequential and parallel codes are developed in FORTRAN for 1D Heat equation for a rod of domain, using MPI protocols. The parallel code is validated using the sequential code by plotting the temperature field at two different times, different parallel performance parameters are recorded in order to justify the code. The point-to-point communication and non-blocking synchronous send is utilised for a parallel MPI code to reduce the cost of communication between boundaries exchange and overall reduction in execution time.

1. Message Passing Interface (MPI):- The sequential algorithms can be run in any processor which support sequential algorithms, but the time consumed using sequential for a bigger problem size are reflected in cost of computation. Hence MPI, which also provides portability of code across different platforms reduces the cost of computation by running particular program across different devices, that is same message passing code can be run on different machines.
Whole domain is decomposed or divided into three equal pieces, that is, ChunkSize = 333 and then mapped with three different processors for computation. In data parallelism, communication between processors for boundary exchange, plays an important role. The code is identical for all the processors, this model is known as Single-Program Multiple-Data (SPMD).

2. Communication Modes:- The parallel program utilises the Non-Blocking communication since I want to reduce the time consumed in boundary exchange. I have variety of communication modes in MPI which have their different criteria for satisfying call completion. The code unitises Synchronous Send and matching Receive. A synchronous mode can be started whether or not a matching receive was posted. However the send will complete successfully only if a matching receive operation has started to receive the message sent by the synchronous send. Thus the completion of a synchronous send not only indicate that the send buffer can be reused but also indicates that the receive has reached a certain point in its execution namely that it has started executing the matching receive

3. Validation of Parallel Code:- Both sequential and parallel codes are run for a total time of 2E-03 and temperature fields are obtained at time T = 2E-04 and T = 2E-05. It can be observe that in parallel and sequential codes, there is very little variation when they compute the temperature field for grid spacing, dx = 0.001. It validates our results since difference between two is more then 1E-10.

  The most important performance evaluation parameter in a parallel program is the execution time, also known as wall-clock time, execution time refers to the time elapsed since first processor starts computation to the last processor completes the computation.

  The computation time is negligible small since we are using non-blocking synchronous send, which calls an MPI routine to setup a communication (send or receive), but routine returns before the communication has completed. The communication then keep on continuing in the background and the process can carry on with other works. Hence, by using Non-blocking communication we try to minimize the communication cost between the boundaries to the minimum, therefore it is not included in this analysis.

4. Conclusion:- The given 1D heat equation is discretised and sequential code is developed, which then converted into parallel code using MPI protocols. The parallel code developed using sequential, seems working by utilising all the three processors one after another. Practically, sequential calling of processors one after another takes more time than the sequential code but it would reduce the CPU time considerably. However, it must be noted that this code could be further refined by using collective communication instead of point-to-point communication. The collective communication allows using of all the three processors in various ways, for example, one-to-serval or serval-to-one this would reduce the serval point-to-point calls and simplifies the code further, thus leading to reduction execution time which leads to reduced cost of communication.