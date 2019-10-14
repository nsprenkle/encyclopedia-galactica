# Java

## Documentation - Javadoc

[How to write JavaDoc comments](http://www.oracle.com/technetwork/articles/java/index-137868.html)


## Testing - JUnit

## Mocking - Mockito

## Spring

Spring is a dependency injection (DI) framework with a handfull of other modules/spinoff projects designed to make development in Java simpler.

## Spring Batch

https://docs.spring.io/spring-batch/4.0.x/reference/html/step.html#configureStep
https://www.dineshonjava.com/configuring-step-in-spring-batch-2/
https://www.toptal.com/spring/spring-batch-tutorial
http://techie-mixture.blogspot.com/2016/07/passing-values-between-spring-batch.html

Job : template

Job Instance : one job to do

Job Execution: one attempt at that job

Job Parameters: params for running a job instance

Step: a part of a job (should be retryable)

Step Execution: one attempt at a step

https://www.tutorialspoint.com/spring_batch/spring_batch_architecture.htm

3 Layers
  - Application: jobs & code
  - Batch Core: API for control/launch of batch job
  - Batch Infrastructure: readers, writers, and services, used by the above two

Steps have
  - Reader: take input data (DB)
  - Processor (opt): datatype conversion
  - Writer: send to output (DB)