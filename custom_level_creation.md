# Custom level creation in Turing Complete (*VERY ALPHA*)

This document is intended to record directions and notes posted to Discord by Stuffe and others regarding custom level creation.

## Table of Contents

- [Preparation](#preparation)
- [Getting Started](#getting-started)
- [Default Level Layout](#default-level-layout)
- [Level Metadata](#level-metadata)
- [Level Testing](#level-testing)
- [UI Metadata](#ui-metadata)
- [Adding your level to the map](#adding-your-level-to-the-map)

## Preparation

1. Use your favorite git tool to fork the main tc_campaign repository from https://github.com/Stuffe/tc_campaign.
2. Make sure TC is closed and that Steam has completed its cloud sync (if enabled).
3. Navigate to your TC installation directory.
    - If you are using Steam, you can right-click TC and select Properties->Installed Files->Browse.
4. Delete the existing `campaign` directory (you can always reinstall via Steam if you need, or rename it if you prefer to keep the backup).
5. Clone your fork:
    - `git clone https://<your repository>/tc_campaign.git campaign`

You should now be able to start TC with the newly-cloned campaign.

> **CAUTION**: It is highly recommended that you push local commits to your fork regularly in order to avoid Steam updates overwriting files unexpectedly, or otherwise conflicting with your changes.
>
> Alternatively, you can disable Steam's automatic updates if you want better control over the timing of your pushes (but still remember to push before doing a manual update!)

## Getting Started

The easiest starting point is to simply copy an existing level that is similar in style to what you're trying to create.

Each level is stored in a separate directory, which contains several common files, which will be described in more detail in following sections:
- [`circuit.data`](#default-level-layout) is the default level layout to allow initializing new schematics with locked (red) components, suggested components, etc.
- [`meta.txt`](#level-metadata) contains the bulk of the level metadata including the level log, default assembly ISA, default assembly code and other bits and pieces.
- [`test.si`](#test-code) contains the code to run the level tests, written in a custom language referred to as Simplex.
    - Michał Isalski has written a VSCode extension to perform syntax highlighting for Simplex: https://marketplace.visualstudio.com/items?itemName=Michai.tc-si
- [`ui.txt`](#ui-metadata) contains metadata for various UI elements displayed in the bottom panel, such as images to load and text styles.

### Naming convention

Your new level directory should be named in all lowercase, with words separated by underscores (`_`), a style known as "snake case".  This is to ensure maximum compatibility across platform.

The level name shown within the game does not have to be related to the directory name (for example, the `Storage Cracker` level is located in the directory `binary_search`).  It is of course more convenient for everyone if the in-game name and the directory name are connected in an obvious manner.

### Opening the game console

Several steps throughout the level creation process will require you to input commands into the game's console.  To access the console, first open the main menu by clicking the "hamburger" icon (`☰`) in the upper left corner and then press `q`.  A small console window will appear in the upper right where you can enter any required commands.

## Default Level Layout

`circuit.data` is the easiest of the bunch to modify as doing so is mostly the same as creating any other circuit in TC.  If you have already added your level to the map, you can simply click to open it.  Otherwise, you can open it by going the console and running the command `load my_level` (replacing `my_level` with your level's directory name).

> **CAUTION**: This performs a "normal" level load, including loading your current architecture schematic if the level you copied was an architecture level.  Make sure you switch to a new (clean) schematic before creating your default level layout.

If you wish to add locked (red) components, you can go back to the console and run the command `dev_mode on`.  This will enable all available components in the game, including the locked components.

Once you are happy with your layout, you can open the console once more and run the command `save_level` to update your `circuit.data`.

## Level Metadata

Coming "Soon".

## Level Testing

Coming "Soon".

## UI Metadata

Coming "Soon".

## Adding your level to the map

At any time after your level directory is created, load up TC and enter the command `dev_mode on` in the console.  This will enable the component menu on the level map, as well as enabling all available components, including those normally hidden during gameplay.

For our current purposes, we want the component called `Level component` under the `DEV` flyout.  Place the component and rotate it until the lock icon is facing the correct direction.

Your component will now display its name as `Level ''not found` (alongside the level ID).  To fix this, select your new component and open the console (**NOTE**: click the main menu icon to do this - pressing Escape will deselect the component).  Run the command `set_component_string my_level` (replacing `my_level` with your level's directory name).

You can now connect your component to the rest of the level map by drawing wires as normal.  The component will automatically update it's state to yellow (available but not yet completed) as soon as it receives the "on" signal from a prior completed level.  Of course, if you connect it to a level that you have not previously completed, it will remain red (locked).

Once you are satisfied with your level's position and connections, you can access the console once more and run the command `save_level` to update level map's `circuit.data`.

It is recommended that you return to the console and run the command `dev_mode off` after you've completed your updates.  You will not be able to load the level from the map while `dev_mode` is enabled (it selects the component instead).

> **CAUTION**: This is the most likely change to cause conflicts with either Steam updates or git pulls as `circuit.data` is a binary file and automatic merging is not really possible.
>
> You will have to choose between the convenience of simply clicking your level to load it and dealing with potential conflicts when they arise, or waiting until the last minute to update the map and stick with running the `load` command in the console whie you're still working on your level.
