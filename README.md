# Introduction 
This repository stores the multiple DayZ PS4 configs used on the community server "(ANZ) | PVE Weekdays | PVP Weekends | Daily Events | see more @ https://discord.gg/3Z8zFcN".

Just before midnight (23:30 AEST/AEDT) every day (Configs are only applied when server restarts next), these configs are rotated each day for specific events. For example, the Modded branch is uploaded on Sunday @ 23:30, ready for the Monday event 'Modded Mondays'.

Branch | Base | Day | Description 
--- | --- | --- | ---
master | [BohemiaInteractive/DayZ-Central-Economy](https://github.com/BohemiaInteractive/DayZ-Central-Economy) |  | Unmodified config forked directly from Bohemia Interactive (BI), not used directly but to abstract other configs, also used to accept updates from BI
All | master |  | A baseline config that applies to all configs
Base | All |  | A baseline config that applies to all config's, excluding Vanilla.
Vanilla | All | Tuesday | A PvE only day with config similar to official servers.
Wildlife | Base | Wednesday | A PvE only day with boosted bears and wolves
Thirsty | Base | Thursday | A PvE only day with no water in waterbottles, drastically less life (Zombies,Fruit,Veg,Animals)
FrightDay | Base | Friday | A PvE only day using the same reduced life as Thirsty, water back in waterbottles, and Hordes of zombies.
Assuault | Base | Saturday | A PvP day only in red zones.
Funday | Base | Sunday | A PvP day with no rules, encouraging base raiding.
Modded | Base | Monday | A PvE day with boosted loot

# XML Files
## File locations and descriptions
File | Folder | Description 
--- | --- | ---
events.xml | files/db/ | Events that spawn vehicles, wrecks, helis, animals, etc
globals.xml | files/db/ | Settings like login timer, max zombies etc.
types.xml | files/db/ | Used to configure item spawn rates and values. 
cfgeconomycore.xml | files/ | used to configure classes included in the central economy, persistence backups, infected dynamic zones, CE logging and updaters. 
cfgenvironment.xml | files/ | Configuration of the animal herd and their territories.
cfgeventspawns.xml | files/ | Used to define positions (and rotation) for certain types of dynamic events (helicrashes, car spawns,..). 
cfglimitsdefinition.xml | files/ | Contains a definition for tag and category limiters. 
cfglimitsdefinitionuser.xml | files/ | User definitions for the limiters, defined in cfglimitsdefinition.xml. Usually allows a simpler definitions such as Tier234 and so on (to save space in db\types.xml file). 
cfgplayerspawnpoints.xml | files/ | Contains base positions for the player spawn point generation (only for the multiplayer mission). Resulting binary file will be generated into the storage folder during first new-player connection. 
cfgrandompresets.xml | files/ | Definitions of presets for random cargo or attachment spawning. Used in cfgspawnabletypes.xml.
cfgspawnabletypes.xml | files/ | Used to define random contents of cargo (inventory) or random attachments for selected spawnable types (defined in db\types.xml). 
mapclusterproto.xml | files/ | Prototypes for cluster-type map groups (fruit trees, objects that spawn mushrooms,..). Each prototype contains containers with spawn-points for loot. 
mapgroupproto.xml | files/ | Whatever object your event spawns, this file is referenced for the relative loot spawn locations and types of loot


## events.xml
Value | Description
--- | ---
name | Valid event name prefixes include: Vehicle, Static, Loot, Infected, Animal, Ambient, Item and Trajectory.
waves | Unknown
nominal | The maximum amount of zones of this type on the map at once.
min | The minimum amount of zones that will spawn on the map. 
max | The maximum amount of zones that will spawn on the map.
lifetime | After spawned, this is the amount of time they last until despawn IF they are outside 'cleanupradius'
restock | The amount of time that will need to pass before this zone is allowed to spawn again. 
saferadius | Minimum distance from players position that they can spawn.
distanceradius | Minimum distance away from other similar zone of this type.
cleanupradius | If zone is this distance away from player position, they will despawn after lifetime ticks down
flags | All attributes of this flag are unknown.
position | Determines whether distance is counted from player position or from a fixed position
limit | Unknown
active | Enables (1) or Disables (0) this event.
children | Array of the different possible spawns within each event

## types.xml
Value | Description 
--- | ---
nominal | how many items should be aproximately in map
lifetime | lifetime in (seconds) - what is the idle before item abandoned at ground gets deleted
restock | restock is oposite of lifetime - idle before item is allowed to respawn when required
min | minimal count should be available in map
quantmin | Dictates the minimum quantity of consumable within the item. Value=(-1.0%(empty) - 100.0%(full)) This is how many bullets are in an Ammo box, or how much water is in a bottle) 
quantmax | Dictates the maximum quantity of consumable within the item. Value=(-1.0%(empty) - 100.0%(full) This is how many bullets are in an Ammo box, or how much water is in a bottle) 
Cost | cost of item determines its 'value' for players (this serve as priority during respawn and cleanup operation)
Category | The category of an item. Effects on how and where the item spawns. (Weapons, Tools, Containers, Clothes, ect.) 
Useage | The group in which area an item will spawn. (Farm, Industrial, Medic, Hunting, ect.) 
Value | The value group of an item. Effects on how and where the item spawns. (Tier1, Tier2, Tier3, ect.) 

## Possible values for types.xml attributes, case sensitive.
Usage | Category | Value | Tag
--- | --- | --- | ---
Coast | clothes | Tier1 | shelves
Farm | containers | Tier2 | floor
Firefighter | explosives | Tier3
Hunting | food | Tier4
Industrial | tools
Medic | weapons
Military | vehiclesparts
Office
Police
Prison
School
Town
Village

## cfgEconomyCore.xml
Variable | Type | Default | Description
--- | --- | --- | ---
world_segments | Integer | 12 | Defines how in many segments world will be split by CE - this affects save, load, cleanup and other processing events - it's performance wide for huge maps (note that default value is for Chernarus map!) 

[see BI wiki for complete values](https://community.bistudio.com/wiki/DayZ:Central_Economy_Configuration)



# How-To
Spawn more of an item? 

In types.xml, find your item and modify the value of 'nominal'. 


Change how long buried stashes remain on server? 

In types.xml, find "UndergroundStash" and modify the value of 'lifetime' in seconds. 


Exclude buried, stored or items on player from the max/nominal count? 

In types.xml, find your item and modify/add the 'flags' element with an attribute of 'count_in_hoarder' for buried? or 'count_in_cargo' for stored? or 'count_in_player' and change the value to '0' ('1' includes it in the count) 


Make an item spawn at a Heli? 

In types.xml, find your item and modify/add the 'flags' element with an attribute of deloot(dynamic event loot) and change the value to '1' ('0' makes it not spawn at Heli's)

# Discord
Here are some templates to use.
## rules
PvE events, mon - fri, strictly no PvP. Keep an eye on in game messeges to identify running event.

PvP Red zone map

ruin cars if abandoning or stripping

No greifing, including glitching, duping or alt accounts


-except sunday

# DayZ-Central-Economy

## Documentation
See the following pages for more information
- https://community.bistudio.com/wiki/DayZ:Central_Economy_Configuration
- https://community.bistudio.com/wiki/DayZ:Central_Economy_setup_for_custom_terrains
    
## License
Arma and Dayz Public License Share Alike (ADPL-SA)

PLEASE, NOTE THAT THIS SUMMARY HAS NO LEGAL EFFECT AND IS ONLY OF AN INFORMATORY NATURE DESIGNED FOR YOU TO GET THE BASIC INFORMATION ABOUT THE CONTENT OF THIS LICENCE. THE ONLY LEGALLY BINDING PROVISIONS ARE THOSE IN THE ORIGINAL AND FULL TEXT OF THIS LICENSE.

With this license you are free to adapt (i.e. modify, rework or update) and share (i.e. copy, distribute or transmit) the material under the following conditions:

- Attribution - You must attribute the material in the manner specified by the author or licensor (but not in any way that suggests that they endorse you or your use of the material).
- Noncommercial - You may not use this material for any commercial purposes.
- Arma and Dayz Only - You may not convert or adapt this material to be used in other games than Arma and Dayz.
- Share Alike - If you adapt, or build upon this material, you may distribute the resulting material only under the same license.

Full text: https://www.bohemia.net/community/licenses/arma-and-dayz-public-license-share-alike-adpl-sa
