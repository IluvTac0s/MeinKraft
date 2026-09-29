- Durability is negative/zero: item has infinite durability for its uses
- Mining power is negative: it can break any and all blocks associated with taht type/tag
ITEM CONFIGURATION DOCUMENTATION
================================

Item configuration files are JSON files stored in:

assets/configurables/items/

An item represents an object that can be held, used, equipped, or placed in the world.

BASIC ITEM FORMAT
-----------------

Example:

{
  "type": "item",
  "tags": ["pickaxe","tool","diamond_tool"],
  "internal_name": "meinkraft:diamond_pickaxe",

  "capabilities": {
    "can_mine": true,
    "can_hurt": true,
    "equippable": false,
    "usable": false
  },

  "tool": {
    "mining_power": 5,
    "durability": 200,
    "durability_cost": 1
  },

  "combat": {
    "damage": 2
  },

  "appearance": {
    "model_type": "2d",
    "texture": "assets/textures/blocks/placeholders/placeholder_block.jpg"
  }
}

REQUIRED FIELDS
---------------

type
    Must be "item".

internal_name
    The unique internal identifier.

    It must use the namespace:name format.

    Example:

    "meinkraft:diamond_pickaxe"

capabilities
    Defines what the item can do.

appearance
    Defines how the item is displayed.

TAGS
----

The "tags" field identifies the item's categories.

Example:

"tags": ["pickaxe"]

An item may have multiple tags.

Example:

"tags": ["tool", "pickaxe", "mining"]

Tags are used by block minability rules.

CAPABILITIES
------------

The capabilities object contains:

can_mine
    Determines whether the item can mine blocks.

can_hurt
    Determines whether the item can damage entities.

equippable
    Determines whether the item can be equipped as armor.

usable
    Determines whether the item can be used directly.(needs code to be added)

All capability values must be JSON booleans.

Correct:

"can_mine": true

Incorrect:

"can_mine": "true"

TOOL
----

The tool object describes mining behavior.

mining_power
    The item's mining power.

durability
    The maximum number of uses before the item breaks.

durability_cost
    The amount of durability consumed per use.

Example:

"tool": {
  "mining_power": 5,
  "durability": 200,
  "durability_cost": 1
}

A durability cost of 1 means one durability point is consumed for every use.

Different actions may later have different durability costs.

COMBAT
------

The combat object describes the item's attack behavior.

damage
    The amount of damage dealt by the item.

Example:

"combat": {
  "damage": 2
}

The combat object may be omitted for items that cannot hurt entities.

APPEARANCE
----------

The appearance object defines how the item is rendered.

model_type
    Defines the item model.

texture
    Defines the texture path.

CURRENT MODEL TYPES
-------------------

2d
    Displays the item as a flat 2D image.

3d
    Reserved for future three-dimensional item models.

Example:

"appearance": {
  "model_type": "2d",
  "texture": "assets/textures/items/diamond_pickaxe.jpg"
}

At the moment, the diamond pickaxe uses the block placeholder texture:

assets/textures/blocks/placeholders/placeholder_block.jpg

A separate item texture should eventually be added.

OPTIONAL OBJECTS
----------------

The following objects may be omitted when they are not relevant:

tool
    Omit for items that are not tools.

combat
    Omit for items that cannot damage entities.

tags
    Omit if the item does not need category tags.

VALIDATION RULES
----------------

An item loader should reject an item if:

- "type" is missing
- "type" is not include "item"
- "internal_name" is missing
- "internal_name" does not contain a namespace
- "capabilities" is missing
- "appearance" is missing
- "appearance.model_type" is unknown
- A texture path does not exist
- Damage is negative
- A boolean value is written as a string

Correct:

"usable": false

Incorrect:

"usable": "false"

INTERNAL NAME EXAMPLES
----------------------
addon_name:item_name
Correct:

meinkraft:diamond_pickaxe
meinkraft:stick
meinkraft:stone

Incorrect(internal naming, in-game commands can use the first one as long as no to have the same name):

diamond_pickaxe
Diamond Pickaxe
meinkraft/diamond_pickaxe
===