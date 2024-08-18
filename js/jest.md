# jest

## Map src directory in jest config using package.json

Nice and concise import statements like this:

```typescript
@import { FooService } from 'src/core/foo.service';
```

are more readable than the ones that look like this:

```typescript
@import { FooService } from '../../../../core/foo.service';
```

The first option compiles fine when building, but fails when running Jest.

This can be fixed easily by adding a `moduleNameMapper` entry to the Jest
config in package.json:

```json
"moduleNameMapper": {
    "^src/(.*)$": "<rootDir>/$1"
}
```

The full `jest` entry:

```json
"jest": {
  "moduleFileExtensions": ["js", "json", "ts"],
  "rootDir": "src",
  "moduleNameMapper": {
    "^src/(.*)$": "<rootDir>/$1"
  },
  "testRegex": ".spec.ts$",
  "transform": {
    "^.+\\.(t|j)s$": "ts-jest"
  },
  "coverageDirectory": "../coverage",
  "testEnvironment": "node"
}
```

The issue thread is on [Github](https://github.com/nestjs/nest/issues/4953).

#### IMPORTANT

According to the author of NestJs, using absolute imports with `src` included
is not recommended and is considered a bad practice. But it can be helpful to
use them in leagcy projets with a lot messy code and long relative imports.
