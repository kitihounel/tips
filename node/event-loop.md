# Event loop tips

- [A case where microtasks runs before process.nextTick](#a-case-where-microtasks-runs-before-processnexttick)

## A case where microtasks runs before process.nextTick

When a script is run in ESM mode, it happens that microtasks (promise callbacks) are run before process.nextTick
callbacks.

Read more [here](https://medium.com/@nileshjha2k/nodejs-an-interesting-case-where-microtasks-running-before-process-nexttick-b729dd9a5ca3).
