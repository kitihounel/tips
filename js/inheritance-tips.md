# Inheritance tips

- [Constructor in child class](#constructor-in-child-class)

## Optional constructor

If the constructor of a child class does not add any logic, it is not necessary to define it.
In fact, static analysis and code quality tools sometimes flag it as a "useless constructor" and give a warning.

This isllustrated by the following code snippet:

```js
class Base {
  constructor(props) {
    this.props = props;
  }
}

class Child extends Base {
  printProps() {
    console.log(this.props);
  }
}

const c = new Child({
  id: 'foo',
  name: 'bar',
});

console.log(c.props);
```

The output is:

```txt
┌─────────┬────────┐
│ (index) │ Values │
├─────────┼────────┤
│   id    │ 'foo'  │
│  name   │ 'bar'  │
└─────-───┴────────┘
```

The constructor is *inherited* somehow. :smile:

**Source:** [SO](https://stackoverflow.com/questions/53652281) thread.
