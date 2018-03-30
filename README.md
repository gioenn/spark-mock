# SparkUndeployingFrame
A non deploying version of the Spark framework

In this modified version of the Spark framework, we acted on the Core of the framework in order to decouple the phases of
operations scheduling (managed by the scheduler package in the core) and the actual data deployment and computing.

We mainly acted on three different classes, all in their Scala versions:
1) DAGScheduler class: (spark\core\src\main\scala\scheduler\DAGScheduler)
   We first introduced a new variable in the class (line 212: private [scheduler] var mapJobWaiter),
   which is Map that will be later used in order to be able to retrieve, starting from a jobId, it's
   associated JobWaiter.
   The first place where we use the newly created variable is in the submitJob function (line 584:
   def submitJob[T, U]), where we store inside the Map the Id of the job that is being submitted
   and, as soon as it is generated, the associated jobWaiter (line 603 and line 610).
   For the same reason, we store the pair (jobId, jobWaiter) also in the submitMapStage function
   (line 694: def submitMapStage[K, V, C])
   Most of the modification (and the ones that actually allow to decouple the scheduling phase of
   the framework) have been operated on the submitStage function; the reason why whe chose this exact
   point in the scheduling process to implement the decoupling is that, at this point, all the logical
   informations about the DAG structure (Job, Stage, Tasks and RDDs) have already been created and so
   we can provide the same amount of logical informations as if we completed the normal computational
   cycle of the framework; in this function we inserted code from line 955 to line 967 with the intention
   of retrieving the jobWaiter associated with the current job in execution, retrieving
2) JobWaiter class: (spark\core\src\main\scala\scheduler\JobWaiter)
3) RDD class: (spark\core\src\main\scala\rdd\RDD)
