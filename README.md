[README.md](https://github.com/user-attachments/files/33254140/README.md)
# Zelda3 Game Editor

Edit progress, inventory and enemy stats, and warp anywhere, in the snesrev **zelda3** reimplementation.

## Start

Double-click **`Zelda3 Game Editor.exe`** in the zelda3 folder. It opens in its own window and shuts down when you close it.

* It runs with the Python that ships in `assets\`, so there's nothing to install.
* The exe isn't code-signed. The first time, Windows may say "Windows protected your PC". Click **More info → Run anyway**.
* `game_editor\Game Editor.bat` starts the same tool with a console window, which helps if something goes wrong.

## Save file tab: progress and inventory

This tab edits the three save files in `saves\sram.dat`.

* **Equipment and items:** sword, shield, armor, gloves, boots, flippers, Moon Pearl, every item and bottle contents.
* **Stats:** hearts, heart pieces, magic and magic upgrade, rupees, bombs and arrows (with capacity upgrades).
* **Progress:** story stage, world, continue point, follower, pendants and crystals.
* **Dungeons:** map, compass, big key and small keys for every dungeon.
* **Shortcuts:** *Max everything* gives you every item. *Refill* tops up health, magic, bombs and arrows.

**Close the game before saving.** The running game keeps its own copy and would overwrite your changes. The first save keeps the untouched file as `saves\sram.dat.editor-orig`. The editor recalculates the file's checksum and backup copy, so the game accepts it.

## Quick-saves & warp tab

This works on the game's quick-save slots while the game is running:

1. In the game, press **Shift+F1** (up to Shift+F10) while walking around. That writes a quick-save.
2. In the editor, click **Reload** and pick the slot.
3. Choose a warp destination, change items too if you like, and click **Save quick-save + warp**.
4. Back in the game, press **F1** (the same slot). Link is warped instantly.

Destinations:

* **Overworld:** outside any building or dungeon exit.
* **Inside:** any of the game's 133 entrances: dungeons, houses, caves and shops.

The editor sets the Light/Dark World automatically. For Dark World destinations without the Moon Pearl, it warns you that Link will be a bunny.

All 194 destinations were tested by running the game's own code: Link arrives in the right room or on the right overworld screen and can play from there.

* Shops and caves that share an interior lead back to where you warped from when you walk out of them.
* Some swords and items look stale until the area reloads. Use the Save file tab for lasting equipment changes.

Every quick-save edit first copies the old file to `saves\editor-backups\`.

## Enemies tab: enemy stats

* **HP** and **contact damage** for each enemy type. Contact damage is a class; the menu shows how many hearts it costs in green, blue and red mail.
* **Weapon vulnerabilities:** one column per weapon (sword levels, arrows, bombs, rods, medallions and so on). The number picks a damage class; hover to see the damage it deals.
* **Global tables** at the bottom: how much each contact-damage class hurts Link, and how much each weapon does for each class.
* **Bulk HP:** *All HP ×* multiplies every enemy's HP, for example 2 for a harder game.

Saving patches `zelda3.exe` (HP and damage tables) and `zelda3_assets.dat` (weapon vulnerabilities). **Close the game first**, then restart it to see the changes. The originals are kept as `zelda3.exe.orig` and `zelda3_assets.dat.orig`, and **Restore originals** puts the enemy data back.

Notes:

* A few bosses set their health in their own code, so their HP field may not change them.
* Rebuilding or updating `zelda3.exe` removes the enemy patches; just save them again.
* Re-extracting assets (`extract_assets.bat`) resets the weapon-vulnerability data.
