# mount-vue-component

## install

```shell
yarn add mount-vue-component
```

## use

```js
import { mount } from 'mount-vue-component'
import { h } from 'vue'

const comp = {
  props: ['name'],
  setup: (props) => () => h('h1', `Hello, ${props.name}!`),
  unmounted() { console.log("Bye") },
  mounted() { console.log("Hi") }
}
const { vNode, destroy, el } = mount(comp, { props: { name: 'world' } })
```

If the component is defined in a `.vue` file and only created programmatically,
you may need to import and register it to avoid its template being removed from
prod builds during tree shaking.  For example:

```js
import MyComponent from "./MyComponent.vue";
const app = createApp(App).use(router);
app.component("MyComponent", MyComponent);
```

## api

#### `mount(component, { props, children, element, app })`

- `component`: required, the component to be created/mounted
- `props`: props to be passed onto the component, this can include HTML attributes like `id` or `class`
- `children`: components to be rendered as children of `component`
- `element`: if specified, the element to mount the component into, if not specified, a `div` will be created
- `app`: the Vue app instance from `createApp`, if provided will be bound to the component's `appContext`

##### returns `{ vNode, destroy, el }`

- `vNode`: the instance of the component provided
- `destroy`: a function that will unmount and destroy the component
- `el`: will provide the HTML element the component is mounted into
