---
title: Debugging topology synchronization
kind: Documentation
aliases:
  - /configuring/debugging_topology_synchronization/
listorder: 10
---

# debugging\_topology\_synchronization

## Overview

StackState allows automating synchronization of topology, as described in [default synchronization guide](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/configure/default_topology_synchronization/README.md). When customizing a synchronization the result might not be as expected: this page explains several tools for debugging. For more info on individual synchronization concepts, see [synchronization concepts](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/configure/sync/README.md).

## Why are components/elements I expect not in my topology?

If no components appear after making changes in a synchronization, or the data is not as expected, a good starting point is the synchronization main screen:

`https://<my instance>/#/settings/synchronizations`

Based on the information you see here, different actions can be taken:

* If there are errors be sure to check the synchronization logs
* If there are no errors:
  * Make sure you 'restarted' your synchronization in the synchronization screen and sent

    in new data, this is because StackState does not retroactively apply changes

  * Make sure the components/relations you want synchronized has its type mapped in the synchronization configuration \(more on that [here](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/configure/default_topology_synchronization/README.md)\)
  * Make sure data is ending up in StackState. The [StackState CLI](https://github.com/mpvvliet/stackstate-docs/tree/0f69067c340456b272cfe50e249f4f4ee680f8d9/setup/cli/README.md) contains a way to see

    what data ends up on the synchronization topic.

## Checking the synchronization logs

StackState stores logs about synchronization in the folllowing places

`<my_install_location>/var/log/sync/`

This directory contains two log files for each synchronization.

* One of the form

  `exttopo.<DataSource Name>.log`. This one contains information about identity extraction

  and the building of an external topology. This will show:

  * If a relation is connected to a non-existing component.
  * When the synchronization is slow it will discard messages
  * When the idextractor has errors

* Another of the form `sync.<Synchronization Name>.log`. This contains information about

  mapping, templates and merging. This will show:

  * Errors in template/mapping functions
  * Component types which have no mapping

