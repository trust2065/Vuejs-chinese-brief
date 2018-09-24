# 最簡設定
```
<div class="app">
  {{val}}
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var vm = new Vue({
    el: ".app",
    data: {
      val: "value 1"
    }
  });
</script>

```

#基本屬性
```
var vm = new Vue({
  el: "",
  data: {}, //存最簡資料, 可計算出的資料不要放這
  props: {}, //接收外部資料
  methods: {},
  watch: {}, //觀察data, 有變動就會觸發
  computed: {}, //有cache功能, 不能吃參數的擴充變數
  template: {},
  components: {} //元件
});
```


# 常用
```
<a :href="...">Sth</a>

<span @click="clickmethod"></span>

{{sth}}
{{condition ? 'y' : 'n'}} // 只能寫statement, 不能寫expression

<template v-if="condition">
  // sth
</template>

<ul id="example-1">
  <li v-for="item in items" v-if="condition">
    {{ item.message }}
  </li>
</ul>

components: {
  'com1': {
    template': '<div>Hello world</div>'
  }
}

```

# 簡述

## Attribute

```
v-bind:href="..."
:href="..."

// ex:
<a :href="...">Sth</a>
```

## Event

```
v-on:click
@click
ex:
`<span @click="clickmethod"></span>`
```

## Text

```
{{sth}}
{{condition ? 'y' : 'n'}} > 只能寫statement, 不能寫expression
```

## Directive

```
v-if
v-elseif
v-else
```
```
<template v-if="condition">
  
  // sth
  
</template>
```
## Loop

v-for
```
<ul id="example-1">
  <li v-for="item in items">
    {{ item.message }}
  </li>
</ul>
```

# Component

- 把會重複使用的元素包起來

## Global component

```
// 區域性的component
new Vue({
  components: {
    'com1': {
      template': '<div>Hello world</div>'
    }
  }
});

// global component
Vue.component('com-1', {
  template: '<div>Hello world</div>'
});
```

## 根元件、子元件
```
new Vue({});     // 根元件
Vue.component(); // 子元件 
```

- 子元件的data要用function包起來
```
Vue.component('com-1', {
  template: '<div>{{msg}}</div>',
  data: function() {
    return {
      msg: "..."
    }
  }
});
```

## 包裝Component的方式

- 直接放HTML標籤 //簡單的元件可以這樣放(我不喜歡就是了)(類似React 的JSX)
- 用script包起來
- render function (after vue2.0) (和React js的createElement類似的東西, 一般不會用)

- 直接放HTML標籤
```
Vue.component('my-component', {
  template: "<div class="component"> A custom component </div>"
});
```
- 用script包裝
```
<script type"text/x-template" id="my-component">
  <div class="component"> A custom component </div>
</script>

Vue.component('my-component', {
  template: "#my-component"
});


```

note: template的最外層只能有一個元素, 若有多個則要用一個div包起來

## 元件的Life Cycle

無論是根元件和子元件都有生命週期!
- beforeCreate (不太做什麼事)
- created (較常用, 已經有data了才觸發)
- beforeMount (取得$el, 但還沒compile)
- mounted (用compile好的結果, 取代$el的內容)
- beforeUpdate 
- updated
- beforeDestroy
- destroyed

## Props

父component傳到子component的參數

```
// 父Component, 有稱為msg的資料
new Vue({
  el: "#app",
  data: {
    msg: "msg of parent!"
  }
});

// id app的div，能傳資料給所有被div包住的元素 
// 這樣msg這個資料就傳到my-component了
<div id="app">
  <my-component :propsA="msg"></my-component>
</div>

// 子Component的定義
Vue.component('my-component', {
  props: ['parentMsg'],
  template: "#my-component",
  data: function() {
    return {
      msg: "msg of child"
    }
  }
});

// 子component的html定義 
<script type="text/x-template" id="my-component">
  <div class="component">
    <div>
      Parent: {{parentMsg}} //可以看到傳進來的attribute~
    </div>
    <div>
      Child: {{msg}}
    </div>
  </div>
</script>

```

## Props檢查型別

寫一個名為props的物件即可檢查

Vue.component('my-component', {
  props: {
    parentMsg: null, //不檢查
    prop1: Number,
    prop2: [String, Number], //可接受兩種
    prop3: {
      type: Number,
      default: 100,
      required: true
    },
    prop4: {
      validator: function(value) {
        return value>10;
      }
    }
  }
});


## 單向資料流
Props in, Event out
