# TypeScript w Andy

Created by microsoft - excellent support through VSCode\

- All valid JS is valid TS.
- TS is used in development, converted to js for build.
  - All ts is stripped off and converted to js.
  - Similar to scss/ css
- A statically typed language - Can't change type (int, string, etc.) once it is set.
  npm installs: `npm i -g typescript` (global install)

## From the command line

- This creates a typescript compiler (tsc)
  - `tsc` to see all of the methods.
- Doesn't run in Node

## In the IDE

Primitives:

```ts
let username: string = 'Alice';
// Will error out if you try to re-assign this as any other type.
username = 'Bob'; // ok
username = false; // error!

// Multi typing:
let username: string | boolean;
username = 'Bob'; // ok
username = false; // ok
username = 101; // error!

// ts will maintain static typing even if exported.
```

Arrays:

```ts
const nums: number[] = [];
const nums.push(15); // ok
const nums.push('wata'); // error on the push parameters.
const output = nums.pop() // will be typed as number because of nums!

const nums: (number|string)[] =[] // Contents can be number or string.
```

Objects:

```ts
const user: {
  username: string
  password: string
} = {
  username: 'Bill Gates'
  password: 'Doritos' // Has to match typing
  friends:[] // Error if it isn't defined in the user typing
}

//Interfaces - A simpler way to define complex types:
interface User {   // A custom type.
  username: string
  password: string
}

const user: User = {
  username: 'Bill Gates'
  password: 'Doritos'
}

// can apply to arrays to:
const users: User[] = [];
users.push(user); // good - each array element has User type
users.push({}); // Error!
```

```ts
// Nested interfaces

interface Dog {
  breed: string;
  weight: number;
}

interface User {
  username: string;
  password: string;
  pet: Dog;
}
```

Dealing with optional fields:

```ts
interface User {
  id?: number; // for databases etc.
  username: string;
  password: string;
  pet: Dog;
}
```

## Functions:

```ts
// Need to know function name, arguments, return value
const sayHello = (user_name: string, age?: number): string => {
  return `hello ${user_name}`;
};
// Optional parameters have to come last, default values work the same as js but can't be optional.

//Trying to invoke the function with mismatched arguments will give an error explaining the typing difference
```

```ts
//Promises:
const returningPromise = (num: number): Promise<number> => {
  return new Promis((resolve) => {
    resolve(num);
  });
};

returningPromise(42).then((data) => {});
```

```ts
//Callbacks:
interface Dog {
  breed: string;
  weight: number;
  goForAWalk: (distance: number, park: string) => (boolean) // What it accepts => what it returns
}

// ... hard to keep up with Andy here...
const doggo: Dog = {
  breed: 'fast'
  weight: 14
  goForAWalk
}
```

## Initializing projects at TS

In the root of your project `tsc --init` creates a tsconfig.json\
Highlights in the tsconfig.json

- "rootDir" - Where to start looking for files
- "outDir" - Where to put the converted files - maintains the same file structure
- "outFile" - Save all the js to one file
- "allowJS" - lets you work in js - overrides the TS compiler.

Manual compile - Run `tsc` from any folder where it could find the config in the parent.

`tsc --watch` - Auto compiles on save.

## Duck Typing

walks and talks like a duck - Must be a duck.\
If input typing matches with the target there is no reason to reject. The object can have extra keys and will still be accepted as long as the base criteria are met.

## Generics

Don't know what the type will be when the interface is created - like 'any'. Promises are generics - They might return data, errors, bool...

```ts
interface IContainer<T> {
  name: string;
  contents: T;
}

const stringContainer: IContainer<string> = {
  name: 'string container',
  contents: 'hello world',
};
```

Try using TS in future applications - get used to it, it's popular.
