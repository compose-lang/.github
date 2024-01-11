# The Compose language

Compose is a programming language designed to run in [WebAssembly](https://webassembly.org).
Compose can be used to create standalone programs ran using [Wasmer](https://wasmer.io/products/runtime) or [wasmtime](https://wasmtime.dev).
It can also be used to create libraries that can be run in a browser, node.js, deno... in short, any platform that provides a WebAssembly runtime.

There are many tools out there to compile from existing languages to WebAssembly, such as [AssemblyScript](https://www.assemblyscript.org), [Emscripten](https://emscripten.org), [Kotlin KMP](https://kotlinlang.org/docs/wasm-overview.html), [Blazor](https://dotnet.microsoft.com/en-us/apps/aspnet/web-apps/blazor) or [j2wasm](https://github.com/google/j2cl/blob/master/docs/getting-started-j2wasm.md). So one might wonder why _yet a new language_ ?

Apart from AssemblyScript, no existing languages has been designed for WebAssembly. As such, they rely on system features or runtime features that are not available in WebAssembly. The above tooling compensates for that by providing libraries that can be costly to download to a browser, and need to mimic behavior of their native runtime, rather than optimize for WebAssembly.

AssemblyScript is also designed to run in WebAssembly, and they've done impressive pioneering work. However, AssemblyScript is a subset of TypeScript, which is itself a typing layer on top of JavaScript, a language known for its [_originalities_](https://gist.github.com/JakeSidSmith/e38f661a7231a912d2d2d380352664da). We needed a stronger basis for running code in a strictly typed execution engine...

By being a dedicated language, Compose avoids all those pitfalls, and can strictly follow WebAssembly features, such as immutable arrays.
Compose also let developers directly write web assembly code (very much the same way you would write __asm in C).

Finally, Compose provides a solution to the famous [deadly diamond of death](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem) problem.
The solution relies on reified attributes, which are described .

