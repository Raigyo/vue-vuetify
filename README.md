# Vue JS / Vuex - Task manager using Vietify

_October 2021_

> 🔨 From udemy: [Vuetify: Create an App with Vue JS & Vuex - Danny Connel](https://www.udemy.com/course/vuetify-vuejs-vuex).

---

![logo](_readme-img/logo.jpg)

## Vuex

### Store

```js
export default new Vuex.Store({
  state: {
    // we store all datas here
    // they can be accessed from everywhere in the app
  },
  mutations: {
    // methods that change data in the state by triggering/commiting
    // synchronously (we cannot reach an API)
  },
  actions: {
    // can't change data in the state
    // dispatch actions then commit mutations
    // asynchronously (we can reach an API)
  },
  getters: {
    // we can get datas from the state
    // we can change or update datas before making them available for all components
  }
  modules: {
    // we can divide the store in several modules
    // all modules can manage their own states, mutations, options and getters
  },
});
```

### Split modules

```js
const moduleA = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... },
  getters: { ... }
}

const moduleB = {
  state: () => ({ ... }),
  mutations: { ... },
  actions: { ... }
}

const store = new Vuex.Store({
  modules: {
    a: moduleA,
    b: moduleB
  }
})

store.state.a // -> `moduleA`'s state
store.state.b // -> `moduleB`'s state
```

## Why using Vue methods is not always best

### Methods

When you have worked with Vue before, you probably have used regular methods to do your computations.

These methods are declared in the "methods" section of your component and behave just like a regular JavaScript function.

methods: {
formatDate() {
}
}
So what's the problem?
The problem with Vue methods emerges when they are used in parts of your component, that are executed with every re-render of the component itself.

For example, if you need to format a date to use it inside a template:

```vue
<template>
  <p>{{ formatDate() }}</p>
</template>
```

When using methods like this, the method is executed every time the component needs to be rendered. Depending on your component, that can be multiple times per second.

Even if your method is quite fast, that can have a huge performance impact. Not to mention what happens when calling computation heavy methods.

This is where computed properties really shine.

### Computed properties

Computed properties are cached.

We can avoid all the performance issues mentioned by simply using computed properties.

This is because the result of a computed property is cached, as long the values of the properties used inside of the computed property stay the same.

Using the "formatDate" example, the formatting of the date would happen only once, every time the date changes.

Even if the component is re-rendering like crazy in the meantime, the logic is not executed again but the cached result is used.

## Dependancies / Plugins

- [Vuetify](https://vuetifyjs.com/en/): Material Design Framework.

`vue add vuetify`

- [date-fns](https://www.npmjs.com/package/date-fns): date-fns provides the most comprehensive, yet simple and consistent toolset for manipulating JavaScript dates in a browser & Node.js.

`npm i date-fns`

- [vuedraggable](https://www.npmjs.com/package/vuedraggable): Vue component (Vue.js 2.0) or directive (Vue.js 1.0) allowing drag-and-drop and synchronization with view model array.

`npm i vuedraggable`

`npm install --save @/vuedraggable`

- [dannyconnell/localbase](https://github.com/dannyconnell/localbase): A Firebase-Style Database ... Offline! Localbase gives you an offline database with the simplicity & power of Firebase, all stored in the user's browser (in an IndexedDB database).

`npm install localbase --save`

## useful links

- [Make Apps with Danny - Vue.js Basics](https://www.youtube.com/watch?v=O25jFVucQiw)
- [Make Apps with Danny - Vue js Lists & Child Components](https://www.youtube.com/watch?v=VVjHdzRBCrA)
- [Outils de développement Vue 3 | Quoi de neuf?](https://www.youtube.com/watch?v=ZBkZ7apIA_Y)
- [Vuetify roadmap](https://vuetifyjs.com/en/introduction/roadmap/#v30-titan)
- [Computed Props and Watchers — What's the Difference?](https://michaelnthiessen.com/difference-between-computed-property-and-watcher/n)
- [Vue Router](https://router.vuejs.org/installation.html)
- [date-fns: Modern JavaScript date utility library](https://date-fns.org/)
- [Vue.js Computed Properties](https://malcoded.com/posts/vue-computed-properties/)
- [Understanding computed properties in Vue.js](https://blog.logrocket.com/understanding-computed-properties-in-vue-js/)
