## Pamach

Function to match against stuff.

Inspired by:
* [Replacing switch statements with Object literals](https://toddmotto.com/deprecating-the-switch-statement-for-object-literals/)
* [Rust match syntax](https://doc.rust-lang.org/book/match.html)

Load the thing:
```js
const match = require('pamach');
```

Pass some args and spec obj:
```js
const drink = 'coke';

const myDrink = match(drink)({
  coke:    () => { return 'Pssshhh...'; },
  wine:    () => { return 'I like this harvest from summer 1901...'; },
  beer:    () => { return 'After a long day...' },
  default: () => { return 'H20'; },
});

console.log(myDrink); // -> 'Pssshhh...'
```

Multiple arguments:

```js
const firstComponent = 'coke';
const secondComponent = 'vodka';

const cocktail = match(firstComponent, secondComponent)({
  'coke, vodka': () => { return 'Much better together'; },
  'beer, vodka': () => { return 'Are you sure this is a good idea?'; },
  default:       () => { return 'H20'; }    
});

console.log(cocktail); // -> 'Much better together'
```

Accepts anything that implements `.toString`:
```js
const person = {
  firstName: 'Steve',
  lastName: 'Jobs'
  toString: () => { return `${this.firstName} ${this.lastName}` }
};

const collegue = match(person) ({
  'Steve Jobs': () => {
    return { firstName: 'Jonny', lastName: 'Ive' }
  },
  'Fox Malder': () => {
    return { firstName: 'Dana', lastName: 'Scully' }
  }
});

console.log(collegue); // -> { firstName: 'Jonny', lastName: 'Ive' }
```

### API:
#### `match([args])` -> Function
Takes any number of args and returns new function
#### `fn(spec)` -> Any
that takes `spec` object to map `args` separated by `', '` (coma + space) as
key to corresponding function, so value returned by this function becomes the
return value of `fn(spec)`.

If no key found for given set of `args`, `fn(spec)` tries to find default key in
the `spec` object and call its value.

If no `default` key found, `undefined` is returned.

License - MIT
