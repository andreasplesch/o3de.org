---
description: ' Use the PhysX Collider component to define where collision detection
  and response occur in Open 3D Engine. '
title: PhysX Collider
---

{{< preview-migrated >}}

Performance demands in games and real-time applications require physics simulations to be solved in fractions of a second. The PhysX Collider component allows you to specify primitive shapes or PhysX mesh assets to calculate collisions between entities, ensuring fast physics simulation. A simple entity such as a crate might have a single PhysX Collider component, while more complex entities, such as vehicles, might require multiple PhysX Collider components.

**Note**
The PhysX Collider component attached to an entity by itself creates a static (non-moving) entity, such as a wall or a mountain. To create a dynamic (moving) entity, you also need to add a **[PhysX Rigid Body](/docs/user-guide/components/reference/physx/rigid-body-physics/)** component. The **PhysX Rigid Body Physics** component requires either a primitive collider or convex mesh collider. Triangle mesh physics assets work only with static entities.

The PhysX Collider component requires the [PhysX](/docs/user-guide/gems/reference/physics/nvidia/physx/) gem enabled in your project.

For more information, see [Simulating physics behavior with the PhysX system](/docs/user-guide/interactivity/physics/nvidia-physx/).

**Topics**
+ [PhysX Collider properties](#physx-collider-properties)
+ [Static PhysX entities](#static-physx-entities)
+ [Primitive colliders](#primitive-colliders)
+ [Physics asset colliders](#physics-asset-colliders)
+ [Collider component mode](#collider-component-mode)
+ [Colliders as triggers](#colliders-as-triggers)

## PhysX Collider properties 

![\[PhysX Collider component interface.\]](/images/user-guide/component/physx/physx/ui-physx-collider-A.png)

****Collision Layer****
The collision layer that's assigned to the collider. For more information, see [Collision Layers](/docs/user-guide/interactivity/physics/nvidia-physx/configuring/configuration-collision-layers/).

****Collides With****
The collision group containing the layers that this collider collides with. For more information, see [Collision Groups](/docs/user-guide/interactivity/physics/nvidia-physx/configuring/configuration-collision-groups/).

****Trigger****
Set this collider as a trigger. A trigger performs a quick overlap test and does not apply forces or return contact point information. Use this to speed-up PhysX computations where a simple overlap between colliders is sufficient.
Triangle meshes are not supported as triggers.
Trigger Area components cannot be used with PhysX Collider.

****Simulated****
When enabled, this shape collider will be part of the physics simulation.

****In Scene Queries****
When enabled, this shape collider can be queried for raycasts, shapecasts and overlap.

****Offset****
Local offset position of the collider, relative to the entity.

****Rotation****
Local rotation of the collider about the **Offset** of the PhysX collider component.

****Library (Physics Materials)****
The physics material library of the project.

****Slots (Physics Materials)****
Choose a physics material for each material of this collider. A collider can have multiple materials assigned. For more information, see [Physics materials](/docs/user-guide/interactivity/physics/nvidia-physx/materials/).

****Tag****
Set a tag for this collider. Tags can be used to quickly identify components in script or code.

****Rest offset****
PhysX bodies come to rest separated by the sum of their rest offset values. The **Rest offset** value must be less than the **Contact offset** value. Valid values rage from **-Infinity** to **50**.

****Contact offset****
PhysX bodies generate contacts when they are within the sum of their contact offset values. The **Contact offset** value must be greater than the **Rest offset** value. Valid values rage from **0** to **50**.

****Shape****
Shape of the collider. A collider can be a primitive shape or a physics asset.
To use a primitive shape, choose **Box**, **Sphere**, or **Capsule**. For more information, see [Primitive colliders](#primitive-colliders).
To use a physics asset, choose **Physics Asset**. For more information, see [Physics asset colliders](#physics-asset-colliders).

****Physics Asset shape****

![\[PhysX Collider component interface, Physics Asset.\]](/images/user-guide/component/physx/physx/ui-physx-collider-A-0.png)

**PhysX Mesh**
Assign a physics asset to the collider. For more information, see [FBX Settings PhysX export](/docs/user-guide/assets/fbx-settings/physx-export/).

**Asset Scale**
Scale the collider shape independent of the entity.

**Physics Materials from Asset**
When the **Physics Asset** shape is selected, and **Physics Materials from Asset** is enabled, the physics materials for this collider are automatically set based on the Physics Materials from the mesh's PhysX asset (see [FBX Settings PhysX tab](/docs/user-guide/assets/fbx-settings/settings-physx-tab/)). If the physics material doesn't exist in the **Physics Material - Library** the default physics material from **PhysX Configuration** will be used. The physics materials cannot be edited while this option is enabled.

****Sphere shape****

![\[PhysX Collider component interface, Sphere.\]](/images/user-guide/component/physx/physx/ui-physx-collider-A-1.png)

**Radius**
Radius multiplier of the sphere collider. The size of the sphere primitive is the **Radius** multiplied by the largest value in the **Scale** property in the **[Transform](/docs/user-guide/components/reference/transform/)** component.

****Box shape****

![\[PhysX Collider component interface, Box.\]](/images/user-guide/component/physx/physx/ui-physx-collider-A-2.png)

**Dimensions**
Width, depth, and height of the box collider.

****Capsule shape****

![\[PhysX Collider component interface, Capsule.\]](/images/user-guide/component/physx/physx/ui-physx-collider-A-3.png)

**Height**
Height of the capsule primitive shape. The height property of the capsule must be at least twice the radius property. For example, if the radius of the capsule is **5.0**, the minimum height is **10.0**.

**Radius**
Radius of the capsule primitive shape. The radius property of the capsule must be no greater than half the height property. For example, if the height of the capsule is **10.0**, the maximum radius is **5.0**.

****Draw Collider****
Render the collider in the viewport. Enabled by default.

****Edit****
Enable collider component mode to edit properties of the collider in the viewport using manipulators.

## Static PhysX entities 

A PhysX entity that is static can interact with other entities, but doesn't move.

**To create a static PhysX entity**

1. Create an entity.

1. In the **Entity Inspector**, choose **Add Component** and then select **Mesh** component.

1. In the **Mesh** component, choose a mesh asset for the **Mesh asset** property.

1. In the **Entity Inspector**, choose **Add Component** and then select **PhysX Collider** component.

1. In the **PhysX Collider** component, set the **Shape** to **Box**, and edit the **Dimensions** property so the box encloses the mesh asset.

1. Press **Control+G** to enter play mode. Because your entity does not have a **PhysX Rigid Body** component, it is static and does not move.
![\[PhysX Collider component example entity that is static.\]](/images/user-guide/component/physx/physx/ui-physx-collider-B.png)
**Tip**
On the **[Transform](/docs/user-guide/components/reference/transform/)** component, enable the **Static** property. This enables optimizations for static entities.

## Primitive colliders 

When you add the **PhysX Collider** component to an entity, you can specify the following basic collider shapes.
+ **Sphere**
+ **Box**
+ **Capsule**

These primitive shapes don't have an underlying mesh. Because they are defined by dimensions rather than a mesh, they are high-performance colliders and should be used when possible.

## Physics asset colliders 

Physics asset colliders are meshes that are created in a modeling application, or are convex meshes that are automatically generated by the FBX exporter. Because physics asset colliders are more complex than shapes, they are less efficient. Physics asset colliders should be used in cases where collision detection that more closely resembles the complex shape of the visible mesh is required. To generate PhysX collider mesh assets for your project, see [FBX Settings PhysX export](/docs/user-guide/assets/fbx-settings/physx-export/).

**Note**
To define a mesh collider that has varying properties:
Use a third-party content creation tool to define a mesh collider and use the FBX exporter to convert the mesh collider for your project. Mesh colliders created this way can only be added to static entities.
Alternatively, attach multiple **PhysX Collider** components to the entity, and specify different PhysX collider shapes and properties for each component.

**To create a mesh collider**

1. Create an entity.

1. In the **Entity Inspector**, choose **Add Component** and then select **Mesh**.

1. In the **Mesh** component, choose a mesh asset for the **Mesh asset** property.

1. In the **Entity Inspector**, choose **Add Component** and then select **PhysX Collider**.
**Note**
If the asset specified for the **Mesh** component contains a PhysX collider mesh asset, the **PhysX Collider** automatically sets its **Shape** property to **Physics Asset**, and its **PhysX Mesh** property to the PhysX collider mesh asset. If the asset specified for the **Mesh** component contains more than one PhysX collider mesh asset, the first PhysX collider mesh asset found is assigned to the **PhysX Mesh** property.

1. In the **PhysX Collider** properties, ensure that the **Shape** property has **Physics Asset** selected.

1. For **PhysX Mesh**, ensure that the desired PhysX collider mesh asset is selected. Click the **...** button to the right of **PhysX Mesh** to change the mesh asset.
![\[PhysX Collider component properties for asset and PhysX collision mesh.\]](/images/user-guide/component/physx/physx/ui-physx-collider-C.png)
**Note**
To generate PhysX collider mesh assets for your project, see [FBX Settings PhysX export](/docs/user-guide/assets/fbx-settings/physx-export/).
**Example**

   Instead of a primitive shape, the entity has a PhysX collider mesh asset specified for the **PhysX Collider** component.
![\[PhysX Collider component with a custom PhysX collider mesh asset to create a custom collider shape.\]](/images/user-guide/component/physx/physx/ui-physx-collider-D.png)

**Note**
To make an entity dynamic, in the **Entity Inspector**, choose **Add Component** and then select **PhysX Rigid Body Physics** component.
Only primitive shapes and convex meshes can be used for dynamic colliders. If you assign a triangle mesh, the collider won't work. For dynamic objects, be sure to disable the **Static** property of the **Transform** component of your entity.

## Collider component mode 

In collider component mode, you edit colliders with manipulators in the viewport. To enter collider component mode, choose the **Edit** button at the bottom of the PhysX Collider component properties in the **Entity Inspector**.

**Sub component modes**
There are three editing modes available in collider component mode.
+ **Resize** mode, which is unique to each collider type, scales the collider.

   The manipulator displayed in the viewport in resize mode is dependent on the collider shape. For primitive colliders, the resize manipulator handles are represented as black squares. For **Physics Asset** colliders, the resize manipulator is represented as a familiar scale manipulator.
+ **Offset** mode translates the collider relative to its entity transform.
+ **Rotation** mode rotates the collider about the component's **Offset**.

**Resize (Sphere Shape)**
**Sphere** resize mode has one linear manipulator that controls the **Radius** property.

![\[PhysX Collider component mode sphere resize manipulator\]](/images/user-guide/component/physx/physx/ui-physx-collider-E.png)

**Resize (Box Shape)**
**Box** resize mode has six linear manipulators, one on each side of the box. The manipulators control the width, depth, and height **Dimensions** property.

![\[PhysX Collider component mode box resize manipulator\]](/images/user-guide/component/physx/physx/ui-physx-collider-G.png)

**Resize (Capsule Shape)**
**Capsule** resize mode has two linear manipulators. The manipulator at the top of the capsule controls the **Height** property. The manipulator on the side controls the **Radius** property.

![\[PhysX Collider component mode capsule resize manipulator\]](/images/user-guide/component/physx/physx/ui-physx-collider-F.png)

**Resize (Physics Asset Shape)**
**Physics Asset** resize mode has a three axis scale manipulator.

![\[PhysX Collider component mode Physics Asset resize manipulator\]](/images/user-guide/component/physx/physx/ui-physx-collider-H.png)

**Offset**
Offset mode has a three axis translate manipulator.

![\[PhysX Collider component mode offset manipulator\]](/images/user-guide/component/physx/physx/ui-physx-collider-I.png)

**Rotation**
Rotation mode has a three axis rotate manipulator.

![\[PhysX Collider component mode rotate manipulator\]](/images/user-guide/component/physx/physx/ui-physx-collider-J.png)

**Collider component mode hotkeys**
These navigation hotkeys are available in collider component mode.
+ **1** - Resize mode.
+ **2** - Offset mode.
+ **3** - Rotation mode.
+ **Control + Mouse Wheel Up** - Next mode.
+ **Control + Mouse Wheel Down** - Previous mode.
+ **R** - Reset current mode. This is effectively an undo operation. You can step through the Resize, Offset, and Rotation modes and press R to reset changes to the current mode.
+ **Escape** - Exit component mode.

## Colliders as triggers 

Triggers allow colliders to perform efficient overlap tests. Colliders marked as triggers won't have forces applied when they intersect with another collider. This is useful for detecting when something enters a certain area or when two objects overlap. Use Lua or Script Canvas to detect overlap.

**Note**
Because triggers don't perform contact resolution, the contact points between a trigger and another collider aren't available.
Triangle meshes are not supported as triggers.
Trigger Area components cannot be used with PhysX Collider.
