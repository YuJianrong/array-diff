fast-array-diff
======================
[![Build Status](https://travis-ci.org/YuJianrong/fast-array-diff.svg?branch=master)](https://travis-ci.org/YuJianrong/fast-array-diff)
[![Coverage Status](https://coveralls.io/repos/github/YuJianrong/fast-array-diff/badge.svg?branch=master)](https://coveralls.io/github/YuJianrong/fast-array-diff?branch=master)
[![npm version](https://badge.fury.io/js/fast-array-diff.svg)](https://badge.fury.io/js/fast-array-diff)
[![MIT Licence](https://badges.frapsoft.com/os/mit/mit.svg?v=103)](https://opensource.org/licenses/mit-license.php)
[![TypeScript](https://badges.frapsoft.com/typescript/code/typescript.svg?v=101)](https://www.typescriptlang.org/)

```fast-array-diff``` is a npm module to find the common or different parts of two array, it based on the solution of LCS (Longest common subsequence) problems, widely used in diff/patch of two arrays (like diff/patch feature in git).

The algorithm of this module is implemented based on the paper "An O(ND) Difference Algorithm and its Variations" by Eugene Myers, Algorithm Vol. 1 No. 2, 1986, pp. 251-266. The difference of this implementation to the implementation of npm module [diff](https://www.npmjs.com/package/diff) is: the space complexity of this implementation is O(N), while the implementation of ```diff``` is O(ND), so this implementation will cost less memory on large data set. Note: although the time complexity of the implementations are both O(ND), this implementation run slower than the ```diff```.

Installation
---------------------

You can install the module via ```npm```:

```bash
npm install fast-array-diff
```

API
----------------------
* `same(arrayOld, arrayNew, compareFunc?)` - get the LCS of the two arrays.

    Return a list of the common subsequence. Like: ```[1,2,3]```

    *Note: The parameter `compareFunc` is optional, `===` will be used if no compare function supplied.*

* `diff(arrayOld, arrayNew, compareFunc?)` - get the difference the two array.

    Return an object of the difference. Like this:

```js
{
    removed: [1,2,3],
    added: [2,3,4]
}
```

Examples
----------------------

Example for ```same``` on array of number:

```js
var diff = require("fast-array-diff");

console.log( diff.same([1, 2, 3, 4], [2, 1, 4]));
// Output: [2, 4]
```

Example for ```diff``` on array of Object with a compare function

```js
var diff = require("fast-array-diff");

function compare(personA, personB) {
    return personA.firstName === personB.firstName && personA.lastName === personB.lastName;
}

var result = diff.diff([
        {
            firstName: "Foo",
            lastName: "Bar"
        },
        {
            firstName: "Apple",
            lastName: "Banana"
        },
        {
            firstName: "Foo",
            lastName: "Bar"
        }
    ], [
        {
            firstName: "Apple",
            lastName: "Banana"
        },
        {
            firstName: "Square",
            lastName: "Triangle"
        }
    ],
    compare
);

// Result is :
// {
//    removed:[
//        { firstName: 'Foo', lastName: 'Bar' },
//        { firstName: 'Foo', lastName: 'Bar' } 
//    ],
//    added: [ { firstName: 'Square', lastName: 'Triangle' } ] 
// }
```

## License

This module is licensed under MIT.
