# Array View for TypeScript and JavaScript

[![npm](https://img.shields.io/npm/v/@omegion1npm/eveniet-sed-atque.svg)](https://www.npmjs.com/package/@omegion1npm/eveniet-sed-atque)
[![npm](https://img.shields.io/npm/dm/@omegion1npm/eveniet-sed-atque.svg?style=flat)](https://www.npmjs.com/package/@omegion1npm/eveniet-sed-atque)
[![Coverage Status](https://coveralls.io/repos/github/Smoren/@omegion1npm/eveniet-sed-atque-ts/badge.svg?branch=master&rand=123)](https://coveralls.io/github/Smoren/@omegion1npm/eveniet-sed-atque-ts?branch=master)
![Build and test](https://github.com/omegion1npm/eveniet-sed-atque/actions/workflows/test.yml/badge.svg)
[![Minified Size](https://badgen.net/bundlephobia/minzip/@omegion1npm/eveniet-sed-atque)](https://bundlephobia.com/result?p=@omegion1npm/eveniet-sed-atque)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

![Array View Logo](docs/images/logo.png)

**Array View** is a TypeScript library that provides a powerful set of utilities for working with arrays in
a versatile and efficient manner. These classes enable developers to create views of arrays, manipulate data with ease,
and select specific elements using index lists, masks, and slice parameters.

Array View offers a Python-like slicing experience for efficient data manipulation and selection of array elements.

## Features
- Create array views for easy data manipulation.
- Select elements using [Python-like slice notation](https://www.geeksforgeeks.org/python-list-slicing/).
- Handle array slicing operations with ease.
- Enable efficient selection of elements using index lists and boolean masks.

## Installation
```bash
npm install @omegion1npm/eveniet-sed-atque
```

## Quick examples
### Slicing
```typescript
import { view } from "@omegion1npm/eveniet-sed-atque";

const originalArray = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const originalView = view(originalArray);

originalView.loc['1:7:2']; // [2, 4, 6]
originalView.loc[':3']; // [1, 2, 3]
originalView.loc['::-1']; // [9, 8, 7, 6, 5, 4, 3, 2, 1]

originalView.loc[2]; // 3
originalView.loc[4]; // 5
originalView.loc[-1]; // 9
originalView.loc[-2]; // 8

originalView.loc['1:7:2'] = [22, 44, 66];
originalArray; // [1, 22, 3, 44, 5, 66, 7, 8, 9]
```

### Subviews
```typescript
import { view, mask, select, slice } from "@omegion1npm/eveniet-sed-atque";

const originalArray = [1, 2, 3, 4, 5];
const originalView = view(originalArray);

originalView.subview(mask([true, false, true, false, true])).toArray(); // [1, 3, 5]
originalView.subview(select([1, 2, 4])).toArray(); // [2, 3, 5]
originalView.subview(slice('::-1')).toArray(); // [5, 4, 3, 2, 1]
originalView.subview(slice([,,-1])).toArray(); // [5, 4, 3, 2, 1]

originalView.subview(mask([true, false, true, false, true])).apply((x: number) => x * 10);
originalArray; // [10, 2, 30, 4, 50]
```

### Combining subviews
```typescript
import { view, mask, select, slice } from "@omegion1npm/eveniet-sed-atque";

const originalArray = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

const subview = view(originalArray)
  .subview('::2')                                 // [1, 3, 5, 7, 9]
  .subview(mask([true, false, true, true, true])) // [1, 5, 7, 9]
  .subview(select([0, 1, 2]))                     // [1, 5, 7]
  .subview('1:')                                  // [5, 7]

subview.loc[':'] = [55, 77];
originalArray; // [1, 2, 3, 4, 55, 6, 77, 8, 9, 10]
```

### Mask example
```typescript
import { view, mask } from "@omegion1npm/eveniet-sed-atque";

const array1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const array2 = [-1, -2, -3, -4, -5, -6, -7, -8, -9, -10];

const mask = view(array1).is((x: number) => x % 3 === 0);
// MaskSelector([false, false, true, false, false, true, false, false, true, false])

view(array2)
  .subview(mask)
  .applyWith(
    view(array1).subview(mask),
    (lhs: number, rhs: number) => lhs + rhs,
  )
  .toArray();
// [-1, -2, 0, -4, -5, 0, -7, -8, 0, -10]);
```

## Contributing
Contributions are welcome! Feel free to open an issue or submit a pull request on the [GitHub repository](https://github.com/omegion1npm/eveniet-sed-atque).

## License
Array View TS is released under the MIT License.
