![Build](https://github.com/zio/izumi-reflect/workflows/Build/badge.svg)

# izumi-reflect

> @quote: Looks a bit similar to TypeTag

`izumi-reflect` is a fast, lightweight, portable and efficient alternative for `TypeTag` from `scala-reflect`.

`izumi-reflect` is a lightweight model of Scala type system and provides a simulator of the important parts of the Scala typechecker.

## Why `izumi-reflect`

1. `izumi-reflect` compiles faster, runs a lot faster than `scala-reflect` and is fully immutable and [thread-safe](https://github.com/scala/bug/issues/10766),
2. `izumi-reflect` supports Scala.js, Scala Native and will support Scala 3 in immediate future,
3. `izumi-reflect` allows you to obtain tags for unapplied type constructors (`F[_]`) and combine them at runtime.

## Credits

`izumi-reflect` has been created by [7mind](https://7mind.io) to power [Izumi Project](https://github.com/7mind/izumi),
as a replacement for `TypeTag` in reaction to a lack of confirmed information about the future of `scala-reflect`/`TypeTag` in Scala 3 ([Motivation](https://blog.7mind.io/lightweight-reflection.html)),
and donated to ZIO.
This repository contains an independent and more conservative copy of the code comparing to Izumi one.

<p align="center">
  <a href="https://izumi.7mind.io/">
  <img width="40%" src="https://github.com/7mind/izumi/blob/develop/doc/microsite/src/main/tut/media/izumi-logo-full-purple.png?raw=true" alt="Izumi"/>
  </a>
</p>


## Limitations

`izumi-reflect` model of the Scala type system is not 100% precise, but "good enough" for the vast majority of the usecases.

Known limitations are:

1. Type boundaries support is very limited because of a [problematic behavior](https://github.com/scala/bug/issues/11673) of Scala 2.13 compiler,
2. Recursive type bounds (F-bounded types) are not preserved and may produce false positives,
3. Existential types written with `forSome` are not supported and may produce unexpected results,
4. Path-Dependent Types are based on variable names and may cause unexpected results with variables with different names but the same type or vice-versa (vs. Scala typechecker)

## Build

`build.sbt` is generated by [sbtgen](https://github.com/7mind/sbtgen). During development you may not want to mess with ScalaJS and ScalaNative, you may generate a pure-JVM Scala project:

```bash
./sbtgen.sc
```

Once you finished tinkering with the code you may want to generate full project and test it for all the platforms:

```bash
./sbtgen.sc --js --native
sbt +test
```
