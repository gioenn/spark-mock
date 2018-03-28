# SparkUndeployingFrame
A non deploying versione of the Spark framework

This is a modified version of the Spark framework, where we acted on the Core of the framework in order to decouple the phases of
operations scheduling (managed by the scheduler package in the core) and the actual data deployment and computing.

We mainly acted on three different classes, with additional minor changes to many others:
1) DAGScheduler class
2) JobWaiter class
3) RDD class
