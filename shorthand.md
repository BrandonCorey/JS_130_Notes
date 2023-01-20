### Concise Property Initalizaers ###
- Allows you to use a variable as a property value and automatically assigns the name as well
```javascript
function createObj(prop1, prop2) {
  return {
    prop1, // instead of prop1: prop1
    prop2, // instead of prop2: prop2
  }
}
```
