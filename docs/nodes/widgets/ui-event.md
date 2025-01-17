---
{
    "events": [
        {
            "event": "$pageview",
            "payload": "{ page }",
            "description": "Sent whenever a user <i>views</i> a given page on the Dashboard"
        },
        {
            "event": "$pageleave",
            "payload": "{ page }",
            "description": "Sent whenever a user <i>leaves</i> a given page on the Dashboard"
        }
    ]
}
---

<script setup>
    import EventsList from '../../components/EventsList.vue'
    import AddedIn from '../../components/AddedIn.vue'
</script>

# Event `ui-event` <AddedIn version="0.9.0" />

This widget doesn't render any content into your Dashboard. Instead, it listens for user-driven behaviour and events in your Dashboard and emits accordingly into the Node-RED Editor when those events have taken place.

## Events List

Currently, we support the following events:

<EventsList />

### Example: Page View

Each time a user views a page, the `ui-event` node will emit:

```js
msg = {
    topic: '$pageview',
    socketid: '1234',
    socketip: '127.0.0.1'
    payload: {
        page: {
            name: 'Page Name',
            path: '/page/path'
            id: '1234',
            theme: 'dark',
            layout: 'default',
            _groups: []
        }
    }
}
```

## Custom Events

In your own `ui-template` nodes, you can emit custom events that will get captured by any `ui-event` node calling the embeded `$socket` operator directly, for example:

```vue
<v-btn @click="$socket.emit('ui-event', 'custom-event-name', msg)">Send Custom Event</v-btn>
```