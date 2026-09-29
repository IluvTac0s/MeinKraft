BLOCK CONFIGURATION DOCUMENTATION
==================================

Block configuration files are JSON files stored in:

assets/configurables/blocks/

A block describes a voxel that can exist in the world.

BASIC BLOCK FORMAT
------------------

A block must contain the following fields:

"type"
    Must be "block".

"internal_name"
    The unique name used internally by the game.

"model"
    Describes how the block is rendered.

"hardness"
    The base hardness of the block.

"minability"
    Describes which tools can mine the block.

Example:

{
  "type": "block",
  "internal_name": "meinkraft:example_block",

  "model": {
    "type": "texture",
    "directional": false,
    "textures": {
      "all": "assets/textures/blocks/example/example.jpg"
    }
  },

  "interactive": false,
  "hardness": 1,
  "minability": {
    "hardness": 1,
    "tool_tags": ["all", "!hand"]
  },

  "item_texture": "assets/textures/blocks/example/example.jpg"
}

REQUIRED FIELDS
---------------

type
    Identifies the object as a block.

    Valid value:

    "block"

internal_name
    The unique internal identifier.

    It must use the namespace:name format.

    Example:

    "meinkraft:dirt"

model
    Defines the block's rendering model.

hardness
    Defines how hard the block is to break.

    This must be a non-negative number.

minability
    Defines the requirements for mining the block.

item_texture
    The texture used when the block appears as an inventory item.

MODEL
-----

The model object contains:

"type"
    Defines the model type.

"directional"
    Defines whether the block can face different directions.

"textures"
    Contains the texture paths used by the model.

CURRENT MODEL TYPE
------------------

texture
    A normal textured voxel block.

    Example:

    "model": {
      "type": "texture",
      "directional": false,
      "textures": {
        "all": "assets/textures/blocks/dirt/dirt.jpg"
      }
    }

TEXTURE DEFINITIONS
-------------------

The textures object maps block faces to texture files.

The following face names are supported:

all
    Uses one texture for every face.

north
    North-facing side.

south
    South-facing side.

east
    East-facing side.

west
    West-facing side.

up
    Top face.

down
    Bottom face.

side
    Uses one texture for the four horizontal sides.

Example:

"textures": {
  "top": "assets/textures/blocks/grass/grass_top.jpg",
  "bottom": "assets/textures/blocks/dirt/dirt.jpg",
  "side": "assets/textures/blocks/grass/grass_side.jpg"
}

If "all" is provided, it is used for every face unless a more specific face texture is provided.

DIRECTIONAL BLOCKS
------------------

A non-directional block has the following setting:

"directional": false

A directional block has:

"directional": true

Directional blocks may use different models or textures depending on their orientation.

Directional behavior is not fully implemented yet. Until it is implemented, block configurations should use:

"directional": false

INTERACTION
-----------

The "interactive" field determines whether the block can respond to player interaction.

Non-interactive block:

"interactive": false

Interactive block:

"interactive": true

Interactive blocks will eventually define an interaction handler. The handler should be identified by a registered name rather than a source-code file path.

Planned example:

"interaction": {
  "interactive": true,
  "handler": "open_chest"
}

The interaction system is not implemented yet.

HARDNESS
--------

The "hardness" field defines how much explosive power hte block needs to be broken
Example:

"hardness": 5

The value must be zero or greater.

A value of zero may be used for blocks that break immediately.

MINABILITY
----------

The minability object contains:

"hardness"
    The minimum mining power required to break the block.(defined by item/tool/mining_power)

"tool_tags"
    A list of tags that can mine the block.

Example:

"minability": {
  "hardness": 2,
  "tool_tags": ["pickaxe"]
}

The special tag "all" allows every tool type.

Example:

"tool_tags": ["all"]

An exclamation mark means that a tag is excluded.

Example:

"tool_tags": ["all", "!hand"]

This means every tool can mine the block except an empty hand.

ITEM TEXTURE
------------

The "item_texture" field defines the texture used when the block is displayed as an inventory item.

Example:

"item_texture": "assets/textures/blocks/dirt/dirt.jpg"

The item texture system may later support separate item-specific textures.

MISSING BLOCK
-------------

The missing block is used when a block's texture or model cannot be loaded.

Current file:

assets/configurables/blocks/missing.json

The missing block uses the placeholder texture:

assets/textures/blocks/placeholders/placeholder_block.jpg

Example:

{
  "type": "block",
  "internal_name": "meinkraft:missing_block",
  "comment": "Used when a block texture or model is missing",

  "model": {
    "type": "texture",
    "directional": false,
    "textures": {
      "all": "assets/textures/blocks/placeholders/placeholder_block.jpg"
    }
  },

  "interactive": false,
  "hardness": 999999,

  "minability": {
    "hardness": 2,
    "tool_tags": ["all", "!hand"]
  },

  "item_texture": "assets/textures/blocks/placeholders/placeholder_block.jpg"
}

VALIDATION RULES
----------------

A block loader should reject a block if:

- "type" is missing
- "type" is not include "block"
- "internal_name" is missing
- "internal_name" does not contain a namespace, or contains an invalid one(spaces)
- "model" is missing
- "model.type" is unknown
- A texture path does not exist
- A boolean value is written as a string instead of a JSON boolean

Correct:

"interactive": false

Incorrect:

"interactive": "false"
===

- if "hardness" is negative, its assumed infinity is the explosion taht can break it