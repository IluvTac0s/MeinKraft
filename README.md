MEINKRAFT
========

A Minecraft-inspired voxel game written in C++.

PROJECT STATUS
--------------

The project is currently in the initial asset and configuration stage.

Implemented:
- Basic project structure
- JSON-based block configuration
- JSON-based item configuration
- Initial texture asset directories
- Placeholder block texture

Planned:
- Vulkan support
- OpenGL support
- World generation
- Block loading
- Item loading
- Texture loading
- Chunk rendering
- Player movement
- Block interaction
- Inventory system
- Entity system
- Localization
- Game documentation
- ability to add addons

DIRECTORY STRUCTURE
-------------------

assets/
    configurables/
        blocks/
            Block configuration files
        entities/
            Entity configuration files
        items/
            Item configuration files
    localisation/
        Localization files
    textures/
        Block and item textures

src/
    C++ source files

CMakeLists.txt
    Build configuration

icon.jpg
    Project icon

CONFIGURATION FILES
-------------------

Configuration files use JSON.

Every configurable object must have:
- A "type" field
- An "internal_name" field

Internal names use the following format:

namespace:name

Example:

meinkraft:diamond_pickaxe

The namespace identifies the project or mod. The name identifies the object.

Asset paths are written relative to the project root.

Example:

assets/textures/blocks/dirt/dirt.jpg

BLOCKS
------

Block configuration files are stored in:

assets/configurables/blocks/

Example:

assets/configurables/blocks/missing.json

The missing block is used when a block texture or model cannot be loaded.

ITEMS
-----

Item configuration files are stored in:

assets/configurables/items/

Example:

assets/configurables/items/diamond_pickaxe.json

Items can define:
- Mining capabilities
- Combat capabilities
- Tool properties
- Durability
- Appearance
- Tags

TEXTURES
--------

Block textures are stored in:

assets/textures/blocks/

Textures currently use JPEG files. Block textures are expected to use a 16 by 16 pixel resolution, can be more or less.

The placeholder texture is located at:

assets/textures/blocks/placeholders/placeholder_block.jpg

BUILDING
--------

The project uses CMake.

A typical build process is:

mkdir build
cd build
cmake ..
cmake --build .

The exact commands may vary depending on the compiler and generator being used.
