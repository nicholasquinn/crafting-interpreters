# crafting-interpreters
https://craftinginterpreters.com/

## The Front End (Lexing, Parsing, & Static Analysis)

* you start with the user's raw source code i.e. a string of characters
* this string is scanned (technical term is lexing or lexical analysis)
* the lexer (thing that does the lexing) breaks down the string into a series of "words", known as tokens.
    * tokens can consist of a single character or multiple
    * some characters in the source string aren't meaningful, such as spaces or comments, and so are discarded
* the tokens are then parsed. This is where our syntax gets a grammar — the ability to compose larger expressions and statements out of smaller parts.
    * this is similar to how english sentences have grammar, except english is much more complicated than a programming language since it has tons of keywords and exceptions
    * the parser (thing that does the parsing) takes the flat sequence of tokens and generates a tree structure from them. This is referred to as a parse tree, syntax tree, or abstract syntax tree (AST).
        * this tree reflects the nested structure of the grammer, with some tokens being subtokens of others, often recursively.
    * the parser also reports syntax errors
* these first few steps of taking the source code, lexing and parsing it, are pretty common to all languages. At this point we know the syntactic structure of the language, and which expressions are nested in which, but not much else.
* this is where static analysis comes in.
    * the first bit of statis analysis usually done is called binding or resolution. This is where, for each identifier, you find where it's defined and essentially figure out its scope.
    * if the language is statically type, this is also where you type-check i.e. the type is part of the declaration, which can be saved and checked later when trying to do certain things
    * the information found during static analysis is either stored directly in the nodes of the AST, or in a separate lookup table, called a symbol table.
* all steps up until now are considered the front end of the language implementation. The front end of the pipeline is specific to the source language the program is written in.
* The back end is concerned with the final architecture where the program will run.
* In the middle end, the code may be stored in some intermediate representation (IR) that isn’t tightly tied to either the source or destination forms (hence “intermediate”). Instead, the IR acts as an interface between these two languages.
    * This lets you support multiple source languages and target platforms with less effort. Say you want to implement Pascal, C, and Fortran compilers, and you want to target x86, ARM, and, I dunno, SPARC. Normally, that means you’re signing up to write nine full end-to-end compilers (every combination of source -> platform i.e. 3x3)
    * A shared intermediate representation reduces that dramatically. You write one front end for each source language (3) that produces the IR. Then one back end for each target architecture (3). Now you can mix and match those 6 to get every combination.
* you can do optimization on the users source code i.e. replace some heavy mathematical expression that is a constant with just the constant itself at compile time, meaning it doesn't have to evaluate at runtime.
* lastly we do code generation, i.e. generatic the assembly/machine code that the bare metal can actually understand and run.
* you can generate either byte code for a virtual processor architecture, or real machine code for a specific real-world processor architecture. The benefit of the former is portability, where as the latter is performance.
    * if you generate byte code, you also have to write the virtual processor (machine) that is able to understand and run (interpret) this byte code.
* at this point we have reached runtime, where the only other concerns are things like garbage collection if you have automatic memory management and implementation of instanceof type checks if your language supports them.
* 

