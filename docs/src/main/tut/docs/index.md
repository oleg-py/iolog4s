---
layout: docs
title: Getting Started
---

## SBT module ids

```scala
lazy val iolog4s = "iolog4s.org" %% "iolog4s" % "0.0.2"
```

## Constructing a logger

You have three ways of creating a logger:

```scala
import org.iolog4s._
import cats.effect. IO

class Test {
  //this create a logger whose name is the fully qualified name of the enclosing class/object
  val logger1 = Logger.create[IO]

  //logger with a special name
  val logger2 = Logger.create[IO]("special-name")

  //explicit way of doing version 1, or doing some other unholy magic
  val logger3 = Logger.create[IO](this.getClass)


  def logs: IO[Unit] =
    for {
       _ <- logger1.info("This has the name of the enclosing class")
       _ <- logger2.info("This has a special-name")
       _ <- logger3.info("This is just an explicit way of achieving 1")
    } yield ()

}
```