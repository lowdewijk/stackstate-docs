---
title: Script API - Component
kind: Documentation
---

# component

Functions to get access to specific component data.

## Function `withId`

Get access to a component by its id.

**Args:**

* `id` - id of the component we are querying for. Each component has a unique randomly assigned id number. 

**Builder methods**

Each of the methods below give you a Async result with a set of properties

`get` - Gets components details in full with following fields

```text
id
name
description
lastUpdateTimestamp
type
layer
domain
environments
state
runState
outgoingRelations
incomingRelations
synchronized
failingChecks
iconbase64
visible
```

`checks` - Gets a list of component checks each with the following fields

```text
id
lastUpdateTimestamp`
name
description
remediationHint
function
arguments
state
syncCreated
```

`domain` - Gets the domain the component belongs to with the following fields

```text
id
lastUpdateTimestamp
name
description
order
identifier
```

`streams` - Gets a list of component streams each with the following fields

```text
id
lastUpdateTimestamp
name
description
priority
dataType
dataSource
query
```

`type` - Gets the component type of the given component with the following fields

```text
id
lastUpdateTimestamp
name
description
iconbase64
identifier
```

`layer` - Gets the layer for the component with the following fields

```text
id
lastUpdateTimestamp
name
description
order
identifier
```

`environments` - Gets a list of environments this component belongs to with following fields

```text
id
lastUpdateTimestamp
name
description
identifier
ownedBy
```

`propagation` - Get the propagation for the component if any with the following fields

```text
id
lastUpdateTimestamp
function
arguments
```

**Examples:**

This example returns the name of the layer for the component with id `123`. After getting the layer the [AsyncScriptResult](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/develop/scripting/async_script_result/README.md) `then` function is used to get the name of the layer.

```text
Component.withId(123).layer().then { it.name }
```

