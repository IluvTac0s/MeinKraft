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
    The unique name used internally by the game (namespace:name).

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
    Valid value: "block"

internal_name
    The unique internal identifier. It must use the namespace:name format.
    Example: "meinkraft:dirt"

model
    Defines the block's rendering model.

hardness
    Defines how much explosive power the block needs to be broken.
    - Value > 0: Standard hardness.
    - Value = 0: Breaks immediately.
    - Value = -1: Infinite hardness (indestructible).

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

SUPPORTED MODEL TYPES
---------------------

texture
    A normal textured voxel block. "textures" must be an object mapping faces to paths.
    Example:
    "model": {
      "type": "texture",
      "directional": false,
      "textures": {
        "all": "assets/textures/blocks/dirt/dirt.jpg"
      }
    }

unwrap
    A single texture that gets unwrapped onto the block. "textures" must be a string path.
    Example:
    "model": {
      "type": "unwrap",
      "directional": false,
      "textures": "assets/textures/blocks/debug/debug_unwrap.jpg"
    }

TEXTURE DEFINITIONS (for "texture" type)
----------------------------------------

The textures object maps block faces to texture files.

Supported face names:
- all: Uses one texture for every face.
- north, south, east, west: Specific side faces.
- top: Top face.
- bottom: Bottom face.
- side: Uses one texture for the four horizontal sides.

Example:
"textures": {
  "top": "assets/textures/blocks/grass/grass_top.jpg",
  "bottom": "assets/textures/blocks/dirt/dirt.jpg",
  "side": "assets/textures/blocks/grass/grass_side.jpg"
}

DIRECTIONAL BLOCKS
------------------

"directional": false (Non-directional)
"directional": true (Directional)

Directional behavior is not fully implemented. Use "directional": false for now.

INTERACTION
-----------

"interactive": false (Standard block)
"interactive": true (Can respond to player interaction)

The interaction system is not implemented yet.

MINABILITY
----------

The minability object contains:

"hardness"
    The minimum mining power required to break the block.

"tool_tags"
    A list of tags that can mine the block.
    - "all": Allows every tool type.
    - "!tag": Excludes a specific tag (e.g., ["all", "!hand"]).

VALIDATION RULES
----------------

A block loader should reject a block if:
- "type" is missing or not "block".
- "internal_name" is missing, lacks a namespace, or contains spaces.
- "model" is missing or "model.type" is unknown.
- For model type "texture", "textures" is not an object.
- For model type "unwrap", "textures" is not a string.
- A texture path does not exist.
- A boolean value is written as a string (e.g., "false" instead of false).
