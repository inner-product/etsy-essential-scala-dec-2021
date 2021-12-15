# Essential Scala Day 6

```scala
  def bracket[Resource,Result](init: => Resource)(use: Resource => Result)(shutdown: Resource => Unit): Result = {
    val resource = init
    val result =
      try {
        use(resource)
      } finally {
        shutdown(resource)
      }
    result
  }

  bracket(new java.io.File(...))(
    file => doSomething(file)
  )(file => file.delete)
```


```scala
case class JobInfo(author: String, description: String, state: JobState, groupOwnerEmail: String)

trait Job {
  def info: JobInfo
  def job[A]: SparkSession => A
}

theJob: Job
bracket(log(s"Starting ${theJob.info.description}")(_ => theJob.job)(_ => log(s"Shutting down"))
```


```scala
trait GeoIP {
  val fileName = ...

  def distributeFile
}

trait Atlas {
  val fileName = ...

}

class MyStuff extends GeoIP with Atlas {
  // fileName collides

}
```
