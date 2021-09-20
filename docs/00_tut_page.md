# Create a new page

In this tutorial we are going to create a new page inside the Web App.


## Create a component

First of all we start by creating a new Component that we wish to display when navigating to our new page.
We do so by creating a new file called ``NewPageComponent.vue``. For the simplicity of this tutorial, the only contents
of the page should be a headline, welcoming us, and a little lorem ipsum text. We add this to the component as follows:

```html

<template>
<h1>Hey, nice to have you on this page!</h1>
    <p>Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren, no sea takimata sanctus est Lorem ipsum dolor sit amet.</p>
</template>

<script>
export default {
  name: "NewPageComponent"
}
</script>

<style scoped>

</style>

```

## Create a route

Now that we have a component we want to display as a new page, we can define the name of the page and the URL-slug that the
page is connected to. To do so we have to find the ``router.js`` file in ``vue_frontend/src/dashboard/entry/`` and add a route at the end of the list of routes:

```js

...

                {
                    path: "/patients/:id",
                    name: "patient report",
                    props: true,
                    component: () =>
                        import(/* webpackChunkName: "chunk-patients" */ "../views/SinglePatient.vue"),
                },
                {
                    path: "/mynewpage",
                    name: "new page component",
                    component: () =>
                        import(/* webpackChunkName: "chunk-newpage" */ "../views/NewPageComponent.vue"),  // the source depends on the source of your file!
                },

...


```


This change might lead to errors in the Hot Refresh mechanisms, so that it is useful to restart the system. Then you should be able to navigate to 
``localhost:8000/mynewpage``. After these changes you can use the relative path ``/mynewpage`` inside the navigation, sidebar or in links to refer to this newly
created page.

