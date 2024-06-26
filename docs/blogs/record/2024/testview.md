::: details 点击查看
```js
//扩展构造函数
function extend(sup, base) {
  var descriptor = Object.getOwnPropertyDescriptor(
    base.prototype, "constructor"
  );
  base.prototype = Object.create(sup.prototype);
  var handler = {
    construct: function(target, args) {
      var obj = Object.create(base.prototype); //主要在这
      this.apply(target, obj, args);
      return obj;
    },
    apply: function(target, that, args) {
      sup.apply(that, args);//改变this指向，thisArg改为that,并传入全部参数
      base.apply(that, args);
    }
  };
  var proxy = new Proxy(base, handler);
  descriptor.value = proxy;
  Object.defineProperty(base.prototype, "constructor", descriptor);//修复constructor只是惯例，并无真正作用，可以方便扩展无法拿到构造器的原型，通过instance.construct。prototype去设置
  return proxy;
}

var Person = function (name) {
  this.name = name
};

var Boy = extend(Person, function (name, age) {
  this.age = age;
});

Boy.prototype.sex = "M";

var Peter = new Boy("Peter", 13);
console.log(Peter.sex);  // "M"
console.log(Peter.name); // "Peter"
console.log(Peter.age);  // 13
```
:::