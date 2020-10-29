- var app=new Vue({})会自动运行？
```
主要做一些初始化的工作，比如通过lifecycleMixin方法来初始化生命周期。同时看到 Vue 只能通过 new 关键字初始化，然后会调用 this._init 方法，该方法为Vue原型上的方法，接着我们追踪至_init函数。 该方法在 src/core/instance/init.js 中定义。

```
