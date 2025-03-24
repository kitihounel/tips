# Errors

- [Defining custom errors](#defining-custom-errors)
- [Error cause](#error-cause-property)
- [Providing structured data as the error cause](#providing-structured-data-as-the-error-cause)

## Defining custom errors

This is the recommended way to subclass `Error` (and some other types like `Array` and `Map`):

```typescript
class CustomError extends Error {
  constructor(message: string) {
    super(message);
    this.name = 'CustomError';
    Object.setPrototypeOf(this, CustomError.prototype); // This is required to maintain the correct prototype chain
  }
}
```

**Note:** Any subclass of `CustomError` will have to manually set the prototype as well.

To understand why this is needed, read these [notes](https://github.com/microsoft/TypeScript-wiki/blob/81fe7b91664de43c02ea209492ec1cea7f3661d0/Breaking-Changes.md#extending-built-ins-like-error-array-and-map-may-no-longer-work) from the breaking changes in TypeScript 2.1.

There is a good article on [Medium](https://medium.com/@Nelsonalfonso/understanding-custom-errors-in-typescript-a-complete-guide-f47a1df9354c).

## Error `cause` property

The `cause` data property of an `Error` instance indicates the specific original cause of the error.

It is used when catching and re-throwing an error with a more-specific or useful error message in order
to still have access to the original error.

Quote from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error/cause)
page on the cause property:

> The value of cause can be of any type. You should not make assumptions that the error you caught has an Error as its cause, in the same way that you cannot be sure the variable bound in the catch statement is an Error either.

## Example

```js
try {
  connectToDatabase();
} catch (err) {
  throw new Error("Connecting to database failed.", { cause: err });
}
```

## Providing structured data as the error cause

This section is copied from the MDN page mentioned above.

Error messages written for human consumption may be inappropriate for machine parsing &mdash; since they're subject
to rewording or punctuation changes that may break any existing parsing written to consume them. So when throwing
an error from a function, as an alternative to a human-readable error message, you can instead provide the cause
as structured data, for machine parsing.

```js
function makeRsa(p, q) {
  if (!Number.isInteger(p) || !Number.isInteger(q)) {
    throw new Error('RSA key generation requires integer inputs.', {
      cause: { code: 'NonInteger', values: [p, q] },
    });
  }

if (!areCoprime(p, q)) {
    throw new Error('RSA key generation requires two co-prime integers.', {
      cause: { code: 'NonCoprime', values: [p, q] },
    });
  }

  // RSA algorithm…
}
```
