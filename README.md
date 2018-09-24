# 最簡設定
```
<div class="app">
  {{val}}
</div>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
<script>
  var app = new Vue({
    el: ".app",
    data: {
      val: "value 1"
    }
  });
</script>

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


## 其他工具:
- computed: 有cache功能, 不能吃參數的擴充變數
- methods: 方法, 可以在html指定

