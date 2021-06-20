Vue.js is a JavaScript Framework that enables for creating user interfaces. It consists of HTML, CSS and JS and allows to extend HTML with HTML attributes that are called directives. These directives offer functionality and can be either built-in like for-loops or user-defined.

Vue.js itself is focused on the view layer. However with officially maintained packages, functionality for state-management, routing or build automation it can be extended.


### Components

Components are reusable instances in Vue.js. Once created, they can be imported and used in the template
of other components.

A simple example of a component would look like this:

```html

<template>
<h1>This is an example component!</h1>
</template>

<script>
export default {
  name: 'foo-bar',
  data(){
    return{}
  }
}
</script>

<style scoped>

</style>

```

Components typically consist of these sections: 

* Template section: HTML Markup with Vue.js components
* Script section: "Vue.js logic" -> All the data, methods and lifecycle logic live here
* Style section: Not mandatory, but possible for e.g. scoped styling for the specific component

With this component created, it can now be used like so in any other template:

```html
<div id="components-demo">
    <foo-bar></foo-bar>
    <h2>Something here..</h2>
</div>

```

More on components is to be found in the official Vue.js documentation: [https://vuejs.org/v2/guide/components.html](https://vuejs.org/v2/guide/components.html)

---

### Directives

A minimal working example for the built-in directive that equals a _for-loop_ looks like the following:

```html
<ul>
  <li v-for="item in items">{{item.text}}</li>
</ul>
```

The directive is called ``v-for`` and in this example iterates over the list object **items**. each individual object
is assigned by the name _item_ that is defined here. Within the html list tag the ``{{item.text}}`` is a statement to access the _text_ attribute of the _item_ object.

The result of this would show a list of items with their _text_ attributes, like the following:

- foo
- bar
- foobar
- bazbaz

### Routing
To be able to see different views in the browser, it is important, to map created components to routes.
For example a component ``Foo.vue`` would be mapped to the route ``/foo`` and ``Bar.vue`` might be mapped 
to ``/bar``. This would look something like this:

```javascript
const routes = [
    { path: '/foo', component: Foo },
    { path: '/bar', component: Bar }
]
```

This will make sure, that the ``Foo`` component will be rendered, when we are navigating to ``www.example.com/foo``.

The router of this application is to be found in ``vue_frontend/src/dashboard/entry/router.js``. In addition to the simple
mapping of routes and components, it is possible and also sometimes necessary to provide some business logic inside the router.
For instance it is possible to make sure, that an unauthorized user is being redirected to the ``/login`` route.

More on the vue-router is to be found at the official documentation: [https://router.vuejs.org/guide/](https://router.vuejs.org/guide/)

---

### State-management

This application uses the state management pattern/library vuex, which is the official supported state management for Vue.js.
Vuex provides a centralized store for all the data of the application and therefore for all the different components, so that
the data can be managed centralized. There are rules, ensuring, that the state can only be modified predictably.

The following diagram by Vuex/Vue.js gives an overview of the workflow with vuex: 

![https://vuex.vuejs.org/vuex.png](https://vuex.vuejs.org/vuex.png)

The communication between the front end and therefore the store and the Back-end API only happens through so called _actions_, 
which are defined in the state-management. Changes will be then commited to _mutations_ which will then mutate the _state_.
The _state_ is what is rendered inside the components. Whenever a state of some data is changing, the component will be re-rendering,
as long as the principles of Vue.js and vuex are kept.

Inside vue components again, it is possible to trigger/dispatch such an action, that then again connects to a back-end API.

More on vuex is to be found on the official documentation: [https://vuex.vuejs.org/#what-is-a-state-management-pattern](https://vuex.vuejs.org/#what-is-a-state-management-pattern)



---


### Static files / Deploying .vue files

To be able to display ``.vue`` files in a browser, they have to be converted to _static files_, i.e. HTML, CSS and JS source files.
This is happening by running the ``npm run build`` command. This triggers _webpack_, which bundles the ``.vue`` files to be deployed.
See [https://webpack.js.org/](https://webpack.js.org/) for more information.