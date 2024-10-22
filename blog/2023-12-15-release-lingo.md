---
slug: lingo
title: "The Lingo Package Manager"
authors: [tassilo, lhstrh]
tags: [lingo, lingua franca, packaging, build tool]
---

![Banner](../static/img/blog/lingo-release-post.png)

Programming languages like Python, Rust, or JavaScript are popular not only because of particular language features, but also thanks to the quality of the tools and packages they offer access to.
A good and mature ecosystem includes features such as developer support, mainly through IDEs or LSPs. Lingua Franca already shines in this area with its VSCode integration that offers functionality like code highlighting, error handling, build support, and diagram synthesis. Another important aspect of a modern language's ecosystem concerns package management. Although it is possible to import reactors from files in the local file system, support for packaging in Lingua Franca is still in its infancy.

{/* truncate */}

The Lingua Franca team is therefore pleased to present **Lingo**, a new package manager and build tool for Lingua Franca. While we still have a long list of features that we want Lingo to have (including the ability to publish packages), you can already do quite a few useful things with it.
For instance, you can easily set up new Lingua Franca projects with `lingo init --language`, which creates a `Lingo.toml` and a small hello world program under `src/Main.lf`. The `Lingo.toml` specifies a set of apps that are executable LF programs. Apps can be configured with additional build and target properties.

```toml
[package]
name = "Showcase"
version = "0.1.0"

[properties]

[[app]]
name = "Main"
main = "./src/Main.lf"
target = "Cpp"
platform = "Native"

[app.dependencies]

[app.properties]
```

To build this app, simply run `lingo build` and Lingo will start building all the apps specified in the Lingo.toml. You can then find your build result in `./target/bin/Main` or simply run `lingo run` if you want to execute the result. The command `lingo clean` is available for cleaning up build items.

Lingo uses an internal concept called backends to wrap the different tool chains of targets. At the moment there is a `CMake` (Cpp), `pnpm`, `npm` (Typescript) and a `lfc` backend, but the `lfc` backend is a temporary solution until a backend is written for all the different toolchains. Therefore, it is important to know that not all targets and functions are officially supported yet. Especially the creation of federated or embedded programs is not yet supported.

We highly encourage the use of Lingo as it already improves the quality of life when developing LF applications and gives us valuable insights into the needs of developers. But you may be wondering how you can get Lingo. Lingo is published on crates.io. To install it, simply run:

```
cargo install lingua-franca
```

and `lingo` should show up in your `$PATH`. If you have a question, problem or bug, please submit a issue [here](https://github.com/lf-lang/lingo/issues).
