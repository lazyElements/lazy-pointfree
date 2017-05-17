# 基於Polymer Pointfree style

## 實驗中 :D , 先從語法糖開始

## Example

```
// 一個參數的情況下(ex1.html)
// [[sum(items)]]
get sum() {
  return this.compose(
    this.sum
  )
}

//複合參數的情況下 (此案例將計算大於num之陣列總合)
//[[sum(items, num)]]
sum(items, num){
  return this.compose(
    this.map(this.gt(num)),
    this.sum
  )(items)
}

```

## API Document

### `compose(fn1, fn2, ... , fnN) => return [last function] `

### `split(sep:String|RegExp)`

### `prop(p:String)`

### `gt(num:Number)`

### `lt(num:Number)`

### `gte(num:Number)`

### `lte(num:Number)`

### `sum(arr:Array[Number])`

### `max(arr:Array[Number])`

### `min(arr:Array[Number])`

### `add(num:Number)`

### `subtract(num:Number)`

### `isNaN(val)`

### `isNull(val)`

### `isUndefined(val)`

### `isEmpty(val)`

### `toArray(Object) => [{key, value}]`

### `filter(fn:Function)`

### `map(fn:Function)`

### `some(fn:Function)`

### `eveny(fn:Function)`