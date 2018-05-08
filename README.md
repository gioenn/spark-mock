# SparkUndeployingFrame
A non deploying version of the Spark framework

N.B = in this early version, you should use fold() instead of reduce() since the second one is unable
      to manage empty collection (which are passed as default in this version of the framework)

In this modified version of the Spark framework, we acted on the Core of the framework in order to decouple the phases of
operations scheduling (managed by the scheduler package in the core) and the actual data deployment and computing.

We mainly acted on three different classes, all in their Scala versions:

1) DAGScheduler class: (spark\core\src\main\scala\scheduler\DAGScheduler.scala)

2) JobWaiter class: (spark\core\src\main\scala\scheduler\JobWaiter.scala)

3) RDD class: (spark\core\src\main\scala\rdd\RDD.scala)
