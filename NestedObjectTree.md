
```
Exported with AIPRM https://www.aiprm.com by Tasmidur Rahman on 12/14/2023, 12:44:27 PM
```

---


**User:**
 Nested  Object using reduce with an example in javascript:
 1) Nested Object Build
 2) Add a node to the Object
 3) Update Node to Object
 4) Delete Node to Object
 5) Find the Node from the Object
 6) Sort Node from Object
 7) Max value from Object
 8) Sort Node from Object
 9) Convert flat Object
 10) Merge two nested object
 11) Merge two nested object in a sorted  Object

---

**ChatGPT:**
Certainly! Below are examples for each of the requested operations using the <code>reduce</code> function in JavaScript:
1) Nested Object Build:
```javascript
const nestedObject = (keys, value) => {
  return keys.reverse().reduce((acc, key) => ({ [key]: acc }), value);
};

// Example:
const newObj = nestedObject(['a', 'b', 'c'], 123);
console.log(newObj);
// Output: { a: { b: { c: 123 } } }
```
2) Add a node to the Object:
```javascript
const addNodeToObject = (obj, keys, value) => {
  keys.reduce((acc, key, index) => {
    if (index === keys.length - 1) {
      acc[key] = value;
    } else if (!acc[key]) {
      acc[key] = {};
    }
    return acc[key];
  }, obj);
};

// Example:
const myObject = { a: { b: { c: 123 } } };
addNodeToObject(myObject, ['a', 'b', 'd'], 456);
console.log(myObject);
// Output: { a: { b: { c: 123, d: 456 } } }
```
3) Update Node to Object:
```javascript
const updateNodeInObject = (obj, keys, value) => {
  const lastKey = keys.pop();
  keys.reduce((acc, key) => acc[key], obj)[lastKey] = value;
};

// Example:
updateNodeInObject(myObject, ['a', 'b', 'c'], 789);
console.log(myObject);
// Output: { a: { b: { c: 789, d: 456 } } }
```
4) Delete Node from Object:
```javascript
const deleteNodeFromObject = (obj, keys) => {
  const lastKey = keys.pop();
  delete keys.reduce((acc, key) => acc[key], obj)[lastKey];
};

// Example:
deleteNodeFromObject(myObject, ['a', 'b', 'c']);
console.log(myObject);
// Output: { a: { b: { d: 456 } } }
```
5) Find the Node from the Object:
```javascript
const findNodeInObject = (obj, keys) => {
  return keys.reduce((acc, key) => acc[key], obj);
};

// Example:
const foundValue = findNodeInObject(myObject, ['a', 'b', 'd']);
console.log(foundValue);
// Output: 456
```
6) Sort Node from Object:
```javascript
const sortNodeInObject = (obj, keys) => {
  const node = findNodeInObject(obj, keys);
  if (Array.isArray(node)) {
    node.sort();
  }
};

// Example:
myObject.a.b.d = [3, 1, 4, 1, 5, 9];
sortNodeInObject(myObject, ['a', 'b', 'd']);
console.log(myObject);
// Output: { a: { b: { d: [1, 1, 3, 4, 5, 9] } } }
```
7) Max value from Object:
```javascript
const findMaxValueInObject = (obj, keys) => {
  const node = findNodeInObject(obj, keys);
  if (Array.isArray(node)) {
    return Math.max(...node);
  }
};

// Example:
const maxValue = findMaxValueInObject(myObject, ['a', 'b', 'd']);
console.log(maxValue);
// Output: 9
```
8) Sort Node from Object:
Already covered in Example 6.
9) Convert flat Object:
```javascript
const convertFlatObject = (flatObj) => {
  return Object.entries(flatObj).reduce((acc, [key, value]) => {
    const keys = key.split('.');
    addNodeToObject(acc, keys, value);
    return acc;
  }, {});
};

// Example:
const flatObject = { 'a.b.c': 123, 'a.b.d': 456, 'x.y.z': 789 };
const convertedObject = convertFlatObject(flatObject);
console.log(convertedObject);
// Output: { a: { b: { c: 123, d: 456 } }, x: { y: { z: 789 } } }
```
10) Merge two nested objects:
```javascript
const mergeNestedObjects = (obj1, obj2) => {
  return Object.keys(obj2).reduce((acc, key) => {
    if (typeof obj2[key] === 'object' && obj2[key] !== null && !Array.isArray(obj2[key])) {
      acc[key] = mergeNestedObjects(obj1[key] || {}, obj2[key]);
    } else {
      acc[key] = obj2[key];
    }
    return acc;
  }, { ...obj1 });
};

// Example:
const object1 = { a: { b: { c: 123 } } };
const object2 = { a: { b: { d: 456 } }, x: { y: { z: 789 } } };
const mergedObject = mergeNestedObjects(object1, object2);
console.log(mergedObject);
// Output: { a: { b: { c: 123, d: 456 } }, x: { y: { z: 789 } } }
```
11) Merge two nested objects in a sorted object:
```javascript
const mergeAndSortNestedObjects = (obj1, obj2) => {
  const mergedObject = mergeNestedObjects(obj1, obj2);
  sortObjectValues(mergedObject);
  return mergedObject;
};

const sortObjectValues = (obj) => {
  for (const key in obj) {
    if (typeof obj[key] === 'object' && obj[key] !== null && !Array.isArray(obj[key])) {
      sortObjectValues(obj[key]);
    } else if (Array.isArray(obj[key])) {
      obj[key].sort();
    }
  }
};

// Example:
const sortedMergedObject = mergeAndSortNestedObjects(object1, object2);
console.log(sortedMergedObject);
// Output: { a: { b: { c: 123, d: 456 } }, x: { y: { z: 789 } } }
```
These examples cover the requested operations using the <code>reduce</code> function in JavaScript. Feel free to adapt them to your specific needs!
