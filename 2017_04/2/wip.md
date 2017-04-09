# Buggy Diary – WIP

## Graphtools

### Handling of meta data

Currently it was rather clunky to change the meta information of a
node. It was only possible to change the meta information of the
graph or change the meta information of the node and then replace
the node manually. This iteration brings a few new functions that
help coping with meta information. Namely

 - `Graph.setNodeMeta`
 - `Graph.removeNodeMeta`
 - `Graph.updateNodeMeta`
 - `Graph.getNodeMeta`

They change the meta information of a node and return the new graph
containing the updated node. Furthermore there is now a distinction
between `set` and `update`. Up to 0.4.0-pre.29 set usually extended
a value if it was an object type. Now set always removes old
values und sets the given value as the meta information
(as indicated by the name and documentation) and update on the other
hand extends object values. Consider the following example:

```
const g1 = Graph.setNodeMeta('key', {a: 'v1'}, 'node', g)
const g2 = Graph.setNodeMeta('key', {b: 'v2'}, 'node', g1)
const g3 = Graph.updateNodeMeta('key', {b: 'v2'}, 'node', g1)
```

In this example the key `key` is set to a new value (`g2`) or
is updated (`g3`). In the first case the value stored at `key`
is only `{b: 'v2'}` and the value for `a` is removed. In the
second case (`g3`) the meta information is updated and the
new value is `{a: 'v1', b: 'v2'}`.