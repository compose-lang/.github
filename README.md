# The Compose language

Compose is a programming language designed to run in [WebAssembly](https://webassembly.org).
Compose can be used to create standalone programs ran using [Wasmer](https://wasmer.io/products/runtime) or [wasmtime](https://wasmtime.dev).
It can also be used to create libraries that can be run in a browser, [node.js](https://nodejs.org/en), [deno](https://deno.com)... in short, any platform that provides a WebAssembly runtime.

There are many tools out there to compile from existing languages to WebAssembly, such as [AssemblyScript](https://www.assemblyscript.org), [Emscripten](https://emscripten.org), [Kotlin KMP](https://kotlinlang.org/docs/wasm-overview.html), [Blazor](https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor) or [j2wasm](https://github.com/google/j2cl/blob/master/docs/getting-started-j2wasm.md). So one might wonder why _yet a new language_ ?

Apart from AssemblyScript, no existing languages have been designed for WebAssembly. As such, they rely on system or runtime features that are not available in WebAssembly. Their tooling compensates for that by providing libraries that can be costly to download to a browser, and need to mimic behavior of their native runtime, rather than be optimized for WebAssembly.

AssemblyScript is also designed to run in WebAssembly, and they've done impressive pioneering work. However, AssemblyScript is a subset of TypeScript, which is itself a typing layer on top of JavaScript, a language known for its [_originalities_](https://gist.github.com/JakeSidSmith/e38f661a7231a912d2d2d380352664da). We needed a stronger basis for running code in a strictly typed execution engine...

By being a dedicated language, Compose avoids all those pitfalls, and can strictly follow WebAssembly features, such as immutable arrays.
Compose also lets developers directly write web assembly code (very much the same way you would write __asm in C).

Finally, Compose provides a solution to the infamous [deadly diamond of death](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem) problem.
The solution is described [here](https://github.com/compose-lang/.github/blob/main/reified-attributes.md). Since this solution is not available in any mainstream language, we needed a new language altogether.

That said, Compose does not introduce new syntax. Rather, it borrows syntax largely from TypeScript. This choice was not based on syntax preferences. Rather we believe there is a strong business case for migrating TypeScript libraries that require improved performance. By closely mimicking TypeScript syntax, Compose makes it easy to migrate these libraries, with improve performance almost for free, thanks to WebAssembly. The migration tool is WIP.

_Disclaimer: Compose is WIP, you are welcome to explore, comment and contribute. But please do not publicly criticize it until it's released 😃 !_

