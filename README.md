# 基於Polymer Pointfree style

## 實驗中 :D , 先從語法糖開始

## Release Note

* Add Curry Method

## How To Use

```
class youDomModule extends lazyPointfree(Polymer.Element){
  get oneParam(){
    return this.pipe(
      fn1,
      fn2,
      fnN
    )
  }

  multiParam(param1, param2){
    return this.pipe(
      fn1,
      fn2,
      fnN
    )(param)
  }
}
```

## How To Extend Method

```
youClass = (su) => class extends lazyPointfree(su) {
  youMethod(){
    return (val) => {
      return val;
    }
  }
}

class youDomModule extends youClass(Polymer.Element){

}

```

## Example

```

//items = [1,2,3,4,5]

[[sumAll(items)]] => 15

[[sumGtNum(items, 3)]] => 9

class extends lazyPointfree(Polymer.Element){

  //省略…

  // 一個參數的情況下(ex1.html)
  // [[sum(items)]]
  get sumAll() {
    return this.pipe(
      this.sum
    )
  }

  //複合參數的情況下 (此案例將計算大於num之陣列總合)
  //[[sum(items, num)]]
  sumGtNum(items, num){
    return this.pipe(
      this.filter(this.gt(num)),
      this.sum
    )(items)
  }
}

```

## TODO
1. 日誌追蹤
2. 更多更多的方法 😂😂

## API Document

### `compose(fn1, fn2, ... , fnN) => return [first fn] `

由右至左執行 result <= fn1 <= fn2 <= fnN <= value;

### `pipe(fn1, fn2, ..., fnN) => return [last fn]`

由左至右執行 value => fn1 => fn2 => fnN => result

### `curry(fn) => function`

將Function Curry化

```
let fn = (a,b,c) => {
  return a*b*c;
}

let curryFn = curry(fn);


console.log(curryFn(1, 2, 3)); //allow 6
console.log(curryFn(1, 2)(3)); //allow 6
console.log(curryFn(1)(2, 3)); //allow 6
console.log(curryFn(1)(2)(3)); //allow 6
console.log("allow", curryFn(1, 2, 3, 4)); //allow 6
console.log("error", curryFn(1)(2)(3)(4)); //Error
```

### `split(sep:String|RegExp) => Array[str, ...]`

### `prop(p:String) => [?]`

### `gt(num:Number) => Boolean`

### `lt(num:Number) => Boolean`

### `gte(num:Number) => Boolean`

### `lte(num:Number) => Boolean`

### `sum(arr:Array[Number]) => Number`

### `max(arr:Array[Number]) => Number`

### `min(arr:Array[Number]) => Number`

### `add(num:Number) => Number`

### `subtract(num:Number) => Number`

### `isNaN(val) => Boolean`

### `isNull(val) => Boolean`

### `isUndefined(val) => Boolean`

### `isEmpty(val) => Boolean`

### `toArray(Object) => Array[{key, value}]`

### `filter(fn:Function) => Array`

### `map(fn:Function) => Array`

### `some(fn:Function) => Boolean`

### `eveny(fn:Function) => Boolean`
