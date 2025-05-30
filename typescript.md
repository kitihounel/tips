# TypeScript tips

- [Coding guidelines](#coding-guidelines)
- [Decorators](#decorators)
- [Compiler options related to path aliases](#compiler-options-related-to-path-aliases)

## Coding guidelines

- [Clean code for TypeScript](https://github.com/labs42io/clean-code-typescript)

## Decorators

- Series of [articles](https://www.wolksoftware.com/blog/decorators-reflection-javascript-typescript) on decorators and metadata.

## Compiler options related to path aliases

The content under this section is copied from TSConfig reference [page](https://www.typescriptlang.org/tsconfig). 

### `rootDir`

Defaults to the longest common path of all non-declaration input files. If `composite` is set, the default is instead
the directory containing the `tsconfig.json file`.

When TypeScript compiles files, it keeps the same directory structure in the ouput directory as exists in the input
directory.

### `baseUrl`

Sets a base directory from which to resolve bare specifier module names. For example, in the directory structure:

```txt
project
├── ex.ts
├── hello
│   └── world.ts
└── tsconfig.json
```

With `"baseUrl": "./"`, TypeScript will look for files starting at the same folder as the `tsconfig.json`:

```js
import { helloWorld } from 'hello/world';

console.log(helloWorld);
```

This resolution has higher priority than lookups from `node_modules`.

**Important**

This feature was designed for use in conjunction with AMD module loaders in the browser, and is not recommended
in any other context. As of TypeScript 4.1, `baseUrl` is no longer required to be set when using [`paths`](#paths).

NestJS make use of `baseUrl` because it uses Webpack for hot reloading in dev mode.

### `paths`

A series of entries which re-map imports to lookup locations relative to the `baseUrl` if set, or to the `tsconfig`
file itself otherwise.

`paths` lets you declare how TypeScript should resolve an import in your `require`/`import`s.

```json
{
  "compilerOptions": {
    "paths": {
      "@app/*": ["./src/app/*"],
      "@config/*": ["./src/app/_config/*"],
      "@environment/*": ["./src/environments/*"],
      "@shared/*": ["./src/app/_shared/*"],
      "@helpers/*": ["./src/helpers/*"],
      "@tests/*": ["./src/tests/*"]
    }
  }
}
```

In this case, you can tell the TypeScript file resolver to support a number of custom prefixes to find code.

You can read more on path [here](https://www.typescriptlang.org/docs/handbook/modules/reference.html#paths).

### `include`

Specifies an array of filenames or patterns to include in the program. These filenames are resolved relative to the
directory containing the `tsconfig.json` file.

### `exclude`

Specifies an array of filenames or patterns that should be skipped when resolving `include`.

**Important**

`exclude` only changes which files are included as a result of the `include` setting. A file specified
by `exclude` can still become part of your codebase due to an `import` statement in your code, a types
inclusion, a `/// <reference ... />` directive, or being specified in the files list.

It is not a mechanism that prevents a file from being included in the codebase - it simply changes what the
`include` setting finds.
