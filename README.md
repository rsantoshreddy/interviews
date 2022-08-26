# interviews

## Get address from any one of the object of the array with destructuring.

```javascript
var users = [
  { name: 'x', address: { pincode: '123' } },
  { name: 'y', address: { pincode: '1234' } },
];
```

## Solution

```javascript
const [userOne] = users;
const { address } = userOne;
const { pincode } = address;
```

## Question

```javascript
let temp = [
  {
    type: 'ULCER',
    prob: 20,
  },
  {
    type: 'DIAB',
    prob: 10,
  },
  {
    type: 'BP',
    prob: 30,
  },
];
```

```javascript
let output = [
  {
    subType: 'ULCER',
    prob: 20,
  },
  {
    subType: 'DIAB',
    prob: 10,
  },
  {
    subType: 'BP',
    prob: 30,
  },
];
```

## Solutions

`javascript const actualOutput = temp.map(({type, ...rest})=>({...rest, subType: type}));`

## Merge below array of objects based on age.

```javascript
var input1 = [
  { name: 'nisum', office: 'kondapur1', age: 10 },
  { name: 'nisum', office: 'kondapur2', age: 20 },
  { name: 'nisum', office: 'kondapur3', age: 40 },
  { name: 'nisum', office: 'kondapur4', age: 5 },
  { name: 'nisum', office: 'kondapur5', age: 1 },
];
```

```javascript
var input2 = [
  { location: 'hyderabad50', age: 50 },
  { location: 'hyderabad10', age: 10 },
  { location: 'hyderabad20', age: 20 },
  { location: 'hyderabad40', age: 40 },
  { location: 'hyderabad5', age: 5 },
  { location: 'hyderabad1', age: 1 },
];
```

```javascript
var output = [
  { name: 'nisum', office: 'kondapur5', age: 1, location: 'hyderabad1' },
  { name: 'nisum', office: 'kondapur4', age: 5, location: 'hyderabad5' },
  { name: 'nisum', office: 'kondapur1', age: 10, location: 'hyderabad10' },
  { name: 'nisum', office: 'kondapur2', age: 20, location: 'hyderabad20' },
  { name: 'nisum', office: 'kondapur3', age: 40, location: 'hyderabad40' },
  { location: 'hyderabad50', age: 50 },
];
```

## Solutions

```javascript
const mergeTwoArrays = (arr1, arr2, key) => {
  const map = {};
  [...arr1, ...arr2].forEach((ele) => {
    if (map[ele[key]]) {
      map[ele[key]] = { ...map[ele[key]], ...ele };
    } else {
      map[ele[key]] = { ...ele };
    }
  });
  return Object.values(map);
};
```
