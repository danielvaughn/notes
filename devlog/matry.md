# Matry

My main side project for several years.
A programming language for UI designers.

---

### Tuesday 09.12.23

I finally got my VSCode extension published.
Initially it's just basic syntax highlighting for tokens.

The plan is to eventually add:
1. Better syntax highlighting for tokens
2. Syntax highlighting for components
3. Syntax highlighting for stories
4. LSP features for tokens
5. LSP features for components
6. LSP features for stories
7. Tokens renderer
8. Components renderer
9. Stories renderer 

Lots of stuff to do.

### Saturday 08.26.23

I created new nextjs project titled `interactive-docs`.
The goal is to create React-rendered examples of Matry.
At the root of the project is a file called `examples.matry` which contain the code samples.

At this point I'm torn between (a) using ANTLR to actually generate the output bundle, or (b) just building fake React renderings that mimic how Matry will work.
