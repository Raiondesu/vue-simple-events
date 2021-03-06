# vue-simple-events
Yet another event management plugin, but WITHOUT Vue instance

## About

This is just a simple class that helps to manage events in a simple way without dependencies. It also supports TypeScript!

And it's really light - <1kb in size!

## Methods

Method   | Params            | Description
-------- | ----------------- | ----------------------------------------------------------------
`vm.$events.emit`   | `event, payload`  | Emit the event with the given payload.
`vm.$events.$emit`  | `event, payload`  | _Alias for `emit`_
`vm.$events.fire`   | `event, payload`  | _Alias for `emit`_
`vm.$events.on`     | `event, callback` | Listen for the event with the given callback.
`vm.$events.$on`    | `event, callback` | _Alias for `on`_
`vm.$events.listen` | `event, callback` | _Alias for `on`_
`vm.$events.once`   | `event, callback` | Listen for the event once, after handling - remove the listener.
`vm.$events.$once`  | `event, callback` | _Alias for `$once`_
`vm.$events.off`    | `event, callback` | Remove event listener(s) for the event.
`vm.$events.$off`   | `event, callback` | _Alias for `off`_
`vm.$events.remove` | `event, callback` | _Alias for `off`_

## Examples

```js
// Import and initialize
import Vue from 'vue'
import EventManager from 'vue-simple-events'

Vue.use(EventManager)
```

```js
/// Component 1

methods: {
  eventHandler(payload) {
    console.log('Yay, events work!', payload);
  }
},
created() {
  this.$events.on('test', this.eventHandler);
  this.$events.once('test', () => console.log('This will be called just once!'));
},
beforeDestroy() {
  this.$events.off('test', this.eventHandler);
}
```

```js
/// Component 2

created() {
  // Emit events
  this.$events.emit('test', 'Hello!');
  // Logs:
  // -> Yay, events work! Hello!
  // -> This will be called just once!

  this.$events.emit('test', 'Hello!');
  // Logs:
  // -> Yay, events work! Hello!
  // (The 'once' handler isn't fired)
}
```
