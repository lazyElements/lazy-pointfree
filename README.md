# 基於Polymer Pointfree style

## 實驗中 :D , 先從語法糖開始

## Release Note

* 新增pipeLogger & composeLogger兩種日誌追蹤的方法
  * 稍微簡短了pipe & compose & pipeLogger & composeLogger的程式
  * 新增 `eq method`
  * 將 Document 修改成 `Hindley-Milner 簽名`
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
1. 更多更多的方法 😂😂

## API Document

### `composeLogger(fn1, fn2, ... , fnN)`
### `compose(fn1, fn2, ... , fnN)`

由右至左執行 result <= fn1 <= fn2 <= fnN <= value;

### `pipeLogger(fn1, fn2, ..., fnN)`
### `pipe(fn1, fn2, ..., fnN)`

由左至右執行 value => fn1 => fn2 => fnN => result

### `curry(fn)`

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

### `split:: String -> String -> [String]`

### `prop:: a -> String -> b`

### `gt:: Number -> Number -> Boolean`

### `lt:: Number -> Number -> Boolean`

### `gte:: Number -> Number -> Boolean`

### `lte:: Number -> Number -> Boolean`

### `eq:: a -> b -> Boolean`

### `sum:: [Number] -> Number`

### `max:: [Number] -> Number`

### `min:: [Number] -> Number`

### `add:: Number -> Number -> Number`

### `subtract:: Number -> Number -> Number`

### `isNaN:: a -> Boolean`

### `isNull:: a -> Boolean`

### `isUndefined:: a -> Boolean`

### `isEmpty:: a -> Boolean`

### `toArray:: a -> [a]`

### `filter:: (a -> b -> [a]) -> [a] -> [a]`

### `map:: (a -> b -> [a]) -> [a] -> [b]`

### `reduce:: (a -> b -> c -> [b]) -> [b] -> a -> b`

### `some:: (a -> b -> [b]) -> [b] -> Boolean`

### `eveny:: (a -> b -> [b]) -> [b] -> Boolean`
