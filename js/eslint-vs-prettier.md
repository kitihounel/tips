# ESLint vs Prettier

## Make them work together

There are a lot of articles that present methods to use them together. Read this LogRocket
[post](https://blog.logrocket.com/using-prettier-eslint-javascript-formatting/) for a detailed
presentation of both tools and learn how to configure them.

However, we prefer [this](https://www.robinwieruch.de/prettier-eslint/) article because it is simple
and straightforward. If you don't want to configure a lot of things and stick to the defaults, we give
here a simple guide.

1. Install `eslint` and `prettier`.

    ```bash
    npm i -D eslint prettier
    ```

2. Then install these two more packages which are in charge of combining Prettier and ESLint:

    ```bash
    npm i -D eslint-config-prettier eslint-plugin-prettier
    ```

    While the former turns off all ESLint rules that could conflict with Prettier, the latter integrates the Prettier rules into ESLint rules.

3. Last but not least, set the Prettier rules in your ESLint configuration. Therefore, create an .eslintrc file in the root directory of your project and give it the following configuration:

    ```js
    'extends': ['prettier'],
    'plugins': ['prettier'],
    'rules': {
      'prettier/prettier': ['error'],
    },
    ```

## Bonus: using Airbnb

There are two options based on your needs:

- `eslint-config-airbnb`, the complete config with rules for JS and React.
- `eslint-config-airbnb-base`, for only JS.

See [here](https://www.npmjs.com/package/eslint-config-airbnb-base) for the installation guide of the `eslint-config-airbnb-base` package.

Afterward, integrate it in your .eslintrc file:

```js
{
  'extends': ['airbnb', 'prettier'],
  'plugins': ['prettier'],
  'rules': {
    'prettier/prettier': ['error'],
  },
}
```

## Final note

You may not need Prettier. Since ESLint can also format code as mentioned in the LogRocket blog post,
you can configure VS Code to use ESLint as code formatter and use a sharable config like the ones provided
by [Airbnb](https://github.com/airbnb/javascript) or [Google](https://github.com/google/eslint-config-google).
