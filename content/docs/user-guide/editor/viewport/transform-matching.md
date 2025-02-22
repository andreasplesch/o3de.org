---
description: ' Match the transform properties for entities in Open 3D Engine. '
title: Matching the Transform
weight: 400
---

{{< preview-migrated >}}

Instead of manually copying values from one entity's position to another, you can use the ditto feature to share an entity's transform data from one entity to another. This feature enables you to duplicate the same transform data for your entities. For example, to make your child entities face the same direction, you can select the entities and use the ditto feature to apply the change to the entities at once.

**To match a transform using the ditto feature**

1. In the viewport, select an entity.

1. Press and hold **Ctrl** and press the middle mouse button on a target entity. After the target is selected, the current selection transform matches that of the target.

   In the following example, the ditto feature shares an entity's orientation with another entity. Both entities have the same value.

   ![Share the transform data from one entity to another using the ditto feature in O3DE.](/images/user-guide/viewportinteractionmodel/viewport-selection-model-13.gif)

## Ditto a Group Selection 

You can use the ditto feature for a group of entities. This makes it easier for you to modify multiple entities at once.

**To match the transform for a group of entities**

1. In the viewport, select a group of entities.

1. Press and hold **Ctrl** and press the middle mouse button to match an entity's transform data to the group manipulator.

   In the following example, you can select entities (a group selection of tires) and use the ditto feature to match a target entity (the car).

   ![Share the transform data from multiple entities to another using the ditto feature in O3DE](/images/user-guide/viewportinteractionmodel/viewport-selection-model-14.gif)

## Ditto a Group Selection to Local Space 

You can ditto a group of entities to local space so that you can modify entities in local space in relation to another entity.

**To ditto a group selection to local space**

1. In the viewport, select a group of entities.

1. Press and hold **Ctrl** and **Alt** and press the middle mouse button to select a target entity. This sets the local space of each entity in the selected group to the target entity that you specified.

   In the following example, select a group of entities and use the ditto feature to set them to the local space of the target entity.

   ![Use the ditto feature to set the local space for a selection of entities to a target entity in O3DE.](/images/user-guide/viewportinteractionmodel/viewport-selection-model-15.gif)


