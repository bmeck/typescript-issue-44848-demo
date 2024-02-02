# Problem

Given a `src/` directory outputting into `dist/` , `package.json#imports/exports` are mistargetted due to TS not rewriting them. This messes up type acquisition etc. while developing in `src/` or running with a TS aware runtime.

# Example solution

We will be using `tsconfig.json` for the UX when dealing with TS source.

We will be using `jsconfig.json` for the UX when dealing with TS output.

Make 2 different package.json files in `src/` and `/` and ensure declaration is emitted as shown in `tsconfig.json`.

In `src/package.json` 
* set `"name"`` for self referencial bare specified
    * set exports for imports to target `src/**` files
* set imports for imports to target `src/**` files

In `package.json`
* set `"name"` for self referencial bare specified
    * set exports for imports to target `dist/**` files
* set imports for imports to target `dist/**` files

Make a `jsconfig.json` file for tools referencing the `dist/**` and not using `tsconfig.json` like VSCode when interacting packages outside `src/`. This will be picked up when in that directory and be separate from the `tsconfig.json`.

NOTE: without `jsconfig.json` the resolution inside of `dist/` for tooling will be incorrect.
