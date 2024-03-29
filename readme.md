# Colonial Partitioning
*Made by mat1432 [Steam](https://steamcommunity.com/id/mat1432/) [GitHub](https://github.com/mat1432/)*

<img src="/thumbnail.png" style="float:right;width:200px;height:200px;" />

Steam Workshop: [https://steamcommunity.com/sharedfiles/filedetails/?id=2905045887](https://steamcommunity.com/sharedfiles/filedetails/?id=2905045887)
Paradox Mods: [https://mods.paradoxplaza.com/mods/55714/Any](https://mods.paradoxplaza.com/mods/55714/Any)

**1.34.X ; This Mod Does Not Need to be Updated!**

This mod allows you to strip away all provinces any of your colonies has, that is in a colony charter outside their capital charter!
No more Brazil and Colombia completely colonizing Peru on an ironman save, you can just strip the lands to your possession and then unpause to create Colonial Peru!

This Mod is completely dynamic and should be compatible with just about every major map mod! Yes, it works on Random New Worlds, Anbennar, BT, Ante Bellum, etc.

This is a cheat mod, but I've included some settings so that it's less cheaty and more like gaming the system.


## This Mod is:
* NOT Achievement Compatible! (Modifies the checksum)
* But will work on an Ironman save.


An event will pop at game start to specify if you want to enable cheaty options or not.

## Diplomatic Actions:
* Can Instant Annex any of your colonies (requires enabling cheats at game start, or 'normal' on non-Ironman saves)
* You can specifically set colonies to be protected from partitioning / instant annex
* You can undo the partitioning of a colony (Only works on or after update 1.0.5 (29 Dec 2022))
* Will only undo lands that are your sovering provinces (Will NOT transfer lands owned by tributaries)

## Partitioning:
* You can specify to skip any colonies that have not yet cored all provinces to at least a territory, (Uncored land does not form colonies)
* You can specify to ignore the colony coring progress and just full core everything (not allowed on Ironman saves, and disabled by 'No Cheats' option at game start)
* **Provinces cannot be taken away from Active Players!**

### Undo Partitioning:
* Accessed by 'Undo Partitioning' Diplomatic Action under Influence Category
* Will return your provinces or colonial provinces that were taken away using one of the mods features.
  * Does not affect lands owned by non colony subjects (Like vassals or PUs)
* Follows the same logic as regular partitioning, and all nations whose lands are taken from during this process will be flagged as partitioned.
* Will only work on colonies partitioned after Update 1.0.5 (29 Dec 2022)
* **Provinces cannot be taken away from Active Players!**

## Multiplayer Safety:
* By default, any colonies that were ever a player will be protected (Can be disabled)
* Any colonies that were ever a player, if partitioned, will Always keep their cores (Including Territorial Cores) & gain Permanent claims on all lost land.

## This did nothing! Why?
The mod follows some logic before it willingly divides your colonies:
* If your colony owns provinces without either a Territorial or Full core, *That colony will be skipped.*
* If your colony is played by a player, *That colony will be skipped.*
* If your colony is protected (by diplo action), *That colony will be skipped.*
These checks are enabled by default, so that as a player you would not ever have to core a colonial region manually (let your colonies do that!).

You can disable or modify these checks in your settings.

## Install and Uninstall Compatibility:
### Forwards Compatability:
* The mod doesn't edit or replace any files, only adds files. It should be forwards compatible with every future update!
### Backwards Compatibility:
* Same as above... The mod is compatible with prior versions, though don't go too far back because I'm not sure how far it is compatible with.
### Save Compatibility:
* No need to worry about uninstalling, the mod only uses country, province and global flags which do not cause any save game damage upon uninstall.
* You can safely use on any active save game and remove later if you wish.

## AI
* The AI will never use this mod or its features!
* If a game is saved with any menu open, the AI will close it without changes.
* If a setup menu is given to the AI through save trickery, the AI will pick 'Normal' for the Cheats Menu and 'Singleplayer' for the MP menu.


## Supported Languages:
* English by [mat1432](https://steamcommunity.com/id/mat1432/)
* German by [Thylon](https://steamcommunity.com/id/thylon125/)

[GitHub Repository](https://github.com/mat1432/colonial_fixes/)
Licensed under the [GNU General Public License v3.0](https://github.com/mat1432/colonial_fixes/blob/main/LICENSE)

The change logs are in English, so far any and all translations of the Change Logs were done via online websites. NONE of the Translators who Volunteered their time are at fault for any imperfections!

Most of the code is for compatibility, fine-tuning, and ease of use.
At its core the code to partition colonies is like this:
```AMPL
colonial_partition = { # decision
    potential = {
        ai = no
        any_subject_country = { is_colonial_nation = yes }
    }
    allow = { always = yes }
    effect = {
        hidden_effect = {
            every_subject_country = {
                limit = { is_colonial_nation = yes }
                every_owned_province = {
                    limit = {
                        NOT = { colonial_region = capital }
                    }
                    if = {
                        limit = { is_core = prev }
                        remove_core = prev
                    }
                    add_core = root
                    cede_province = root
                }
            }
        }
    }
}
```
