---
description: ' Use the Tag component to apply labels to entities in Open 3D Engine. '
title: Tag
---

{{< preview-migrated >}}

Use the **Tag** component to apply one or more labels, or tags, to an entity such as **burning** or **player**. You can use these tags to find or filter entities with particular traits. For example, you can set a weapon to inflict double damage to entities tagged as **burning**.

## EBuses - Request Bus Interface: TagGlobalRequestBus 

Use the following request function with the **TagGlobalRequestBus** EBus interface to communicate with other components of your game.

For more information about using the Event Bus (EBus) interface, see [Working with the Event Bus (EBus) system](/docs/user-guide/engine/ebus/_index.md).

### RequestTaggedEntities 

Handlers respond if they have the tag (listening on the tag's channel). Use `AZ::EbusAggregateResults` to handle more than the first responder.

**Parameters**
None

**Return**
const `AZ::EntityId`

**Scriptable**
Yes

## EBuses - Request Bus Interface: TagRequestBus 

Use the following request functions with the **TagRequestBus** EBus interface to communicate with other components of your game.

For more information about using the event bus (EBus) interface, see [Working with the Event Bus (EBus) system](/docs/user-guide/engine/ebus/_index.md).

### HasTag 

Returns true if the entity has the tag.

**Parameters**
const `Tag&`

**Return**
bool

**Scriptable**
Yes

### AddTag 

Adds the tag to the entity if it didn't already have it.

**Parameters**
const `Tag&`

**Return**
None

**Scriptable**
Yes

### AddTags 

Add a list of tags to the entity if it didn't already have them.

**Parameters**
const `Tags&`

**Return**
None

**Scriptable**
No

### RemoveTag 

Removes a tag from the entity if it had it.

**Parameters**
const `Tag&`

**Return**
None

**Scriptable**
Yes

### RemoveTags 

Removes a list of tags from the entity if it had them.

**Parameters**
const `Tags&`

**Return**
None

**Scriptable**
No

### GetTags 

Gets the list of tags on the entity.

**Parameters**
None

**Return**
const `Tags&`

**Scriptable**
No

The following is an example of script using the **Request Bus Interface**.

```
local enemies = TagGlobalRequestBus.Event.RequestTaggedEntities(Crc32("Enemy"));

local burning = TagComponentRequestBus.Event.HasTag(self.entityId, Crc32("Burning"));
```

## EBus - Notification Bus Interface: TagComponentNotificationsBus 

Use the following request functions with the **TagComponentNotificationsBus** notification bus interface to communicate with other components of your game.

For more information about using the event bus (EBus) interface, see [Working with the Event Bus (EBus) system](/docs/user-guide/engine/ebus/_index.md).

### OnTagAdded 

Notifies listeners about tags being added.

**Parameters**
const `Tag&` - Indicates the tag was added

**Return**
None

**Scriptable**
Yes

### OnTagRemoved 

Notifies listeners about tags being removed.

**Parameters**
const `Tag&` - Indicates the tag was removed

**Return**
None

**Scriptable**
Yes
