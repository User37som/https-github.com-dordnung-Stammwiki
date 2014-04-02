See what has changed between Stamm versions.

## 2.22
- Fixed some possible bugs with admin flags
- Also support "flags" in StammLevels.txt
- Fixed wrong Native Errors
- Moved storage file to sourcemod/data
- Changed loaded text
- Removed loading of all features on late load

## 2.21
- Fixed a problem with the updater, so it updated not on server start

## 2.20
- Really a lot of code improvements
- Easy support of morecolors
- Fixed errors when unloading features
- Added native `STAMM_OnClientGetPoints_PRE`
- Cvars `stamm_oflag` and `stamm_adminflag` can now hold real flag strings
- Reduced file size a lot
- Fixed Database errors
- Removed `sourcemod/Stamm` folder (levels folder inside is now in `cfg/stamm/levels`)
- A level can now have unlimited descriptions
- Fixed converting Bugs
- Added Natives `STAMM_GetTag`, `STAMM_AddCommand`, `STAMM_GetBlockName`, `STAMM_IsAvailable`, `STAMM_IsMoreColorsAvailable`
- Splitted include files
- Added a lot of error handling in includes
- Improved Translations
- Fixed root admins always get highest VIP level
- Using userids for callbacks
- Fixed issue with precaching sounds
- Added notify when receiving points
- Removed unnecessary public methods
- All translations are now client based
- Replaced `STAMM_GetLevel` with `STAMM_GetBlockLevel`
- Added parameters level and oldlevel to forward `STAMM_OnClientBecomeVip`
- Fixed critical timer errors
- Feature overview works now correct
- Added auto open menu again on some clicks
- Fixed some menu items were clickable
- Binded native `STAMM_AddCommand` to forward `STAMM_OnClientRequestCommands`
- Added detection of duplicate features
- Replaced `STAMM_AddFeature` with `STAMM_RegisterFeature`
- Remove `STAMM_AddDescription`, added `STAMM_OnClientRequestFeatureInfo` therefore
- Stamm Chat tag is now changeable
- Added natives `STAMM_PrintToChatEx`, `STAMM_PrintToChatAllEx` and `STAMM_FormatColor`
- Removed Happy Hour table and using a file for it instead
- Added option so that old players are starting to lose points
- And some more Stuff ;)

## 2.18
- Checking for old Stamm Folder
- Changed sound system on csgo (sounds moved to `sound/stamm` instead of
`sound/music/stamm`)
- Fixed double entries in feature list
- Fixed Happy Hour timer errors
- Added back button in level overview menu
- Fixed double loading of stamm

## 2.17
- Renamed `Stamm` folder to `stamm`

## 2.16
- Added Native `STAMM_GetClientBlock`
- Fixed Panel Bugs
- Fixed Missing Admin Column
- Changed Features for `STAMM_GetClientBlock`

## 2.15
- Cvar to Show Stamm Points in a HUD Text for TF2
- Renamed load commands for features
- Save Player also on disconnect
- Cvar to strip VIP Tag
- Cvar to show Points in a menu or in chat
- Hook Convar Changes
- Generate Info Panel with current Stamm Points dynamically
- Only allow to change features a client have
- Only show levels in info panel, that have features

## 2.14
- Fixed VIP Rank Error
- Fixed wrong converting to new Steamid
- Added column admin
- Fixed Array out of bounds error

## 2.13
- Fixed SQL version errors
- Added `sm plugins` loading handle
- Removed stupid error messages
- Set max. levels/features to 100
- Up to 5 descriptions per level
- Removed command !sme
- Added comments to all files
- Lot of code improvements
- Added native `AutoUpdate`
- Set language folder to translations folder instead of `Stamm/translations`
- Don't count bots
- Added cvar stamm_autoupdate

## 2.12
- Added deleting of old inactive players

## 2.11
- Added sql converting from mysql to sqlite or sqlite to mysql

## 2.10
- Lot of code improvements
- All Steamids will be converted to `STEAM_0:`
- Added `STAMM_` prefix to all natives and forwards
- Added a lot of new natives
- Added private VIP's
- Changed color to olive
- Added new server console commands
- Fixed invalid Handle bugs
- Added auto updater
- Added support for late loading
- Fixed SQL errors
- Client points will be saved indirect
- Added AutoExecConfig for automatic cvar append
- Added support for DOD:S
- Added Feature re-/un-/loading 
- Improved feature handling
- Added `blocks`
- Added back button for some menus
- Improved database convertion
- Added auto using of sqlite
- Happy hour now also works after server restart

## 2.04
- Renamed Stamm folder to stamm

## 2.03
- New Features for developers
- Small fixes!

## 2.02
- Fixed bugs with command cvars!

## 2.01
- Fixed a little bug
- Added new cvar stamm_adminflag, to choose the adminflag to access the admin menu

## 2.00
- Change everything to points
- Added new features
- Fixed bugs
- Only leveling
