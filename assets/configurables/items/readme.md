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
  "tags": ["pickaxe", "tool", "diamond_tool"],
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
    The unique internal identifier (namespace:name).

capabilities
    Defines what the item can do.

appearance
    Defines how the item is displayed.

TAGS
----

The "tags" field is a list of strings identifying the item's categories.
Example: "tags": ["tool", "pickaxe"]

Tags are used by block minability rules.

CAPABILITIES
------------

All capability values must be JSON booleans:
- can_mine: Can the item break blocks?
- can_hurt: Can the item damage entities?
- equippable: Can the item be worn as armor?
- usable: Can the item be used directly? (Logic TBD)

TOOL
----

The tool object describes mining behavior:
- mining_power: The power of the tool. A negative value means it can break any block of the associated tag.
- durability: Max uses. A value <= 0 means infinite durability.
- durability_cost: Points consumed per use.

COMBAT
------

- damage: Amount of damage dealt. Must be non-negative.

APPEARANCE
----------

- model_type: "2d" (flat image) or "3d" (reserved).
- texture: Path to the image file.

VALIDATION RULES
----------------

An item loader should reject an item if:
- "type" is missing or not "item".
- "internal_name" is missing or lacks a namespace.
- "capabilities" or "appearance" are missing.
- "appearance.model_type" is unknown.
- A texture path does not exist.
- Damage is negative.
- "tags" is not a list.
- A boolean value is written as a string.

INTERNAL NAME EXAMPLES
----------------------
Correct:
meinkraft:diamond_pickaxe
meinkraft:stick

Incorrect:
diamond_pickaxe
meinkraft/diamond_pickaxe
