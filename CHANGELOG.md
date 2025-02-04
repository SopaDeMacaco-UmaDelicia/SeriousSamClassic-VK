# Changelog
All notable changes to this project will be documented in this file.

## 2021-10-09 - 2021-11-10
- Fixed crash the game when playing the demo with parameter cli_bPrediction=1;
- Fixed attempt to create a udp socket when it is already created
  (the created server stopped responding after the first heartbeat)
- added timeout when reading the response to the master server (setsockopt)
- Increased the CTString PrintF buffer 
  (256 bytes was not enough to form a server response on request \status\,
  look.. CTString.cpp)
- Added \basic\ \info\ \rules\ request
- In GameAgent added support for both TFE and TSE
- In DedicatedServer added support for both TFE and TSE
- Restore green color for TFE (it will be right)
- Enabled building DedicatedServer 
- Added few diagnostic messages
- Fixed bug with loading levels from subdirectories (see IsDirectory() function)
- Added support for 16:9, 16:10, 21:9 screen sides. Fixed menu, NETRICSA, font and HUD for all screen ratios. 
  Fixed the position of the weapon and the player's FOV of view from the first and third person 
  for resolutions 16:9 16:10 21:9 (look 42amsterdam.net fix42 open source mod for a classic sam).
- Added MakeFONT compilation to CMakeLists.txt .
  MakeFONT allows you to create your own fonts for the game.
- Added support for launching mods from the game menu. (look CheckModReload function).
- Deleting using time to get a precision timer for __GNU_INLINE_X86_64__.
  Removing the ugly hack /proc/cpuinfo.
  Adding assembler code to get RDTSC for __GNU_INLINE_X86_64__. 
  Adding several libcpuid functions to get the correct TSC.
  (Note: Using a single RDTSC call in 32-bit mode did not take into account the p-state of the processor, 
  the dynamic frequency of the CPU, and led to different game speeds depending on the current p-state.
  Fixed with a function from libcpuid -  look at Engine\Timer.cpp.
  Using time instead of RDTSC In 64 mode broke the menu, 
  dynamic displays of enemy models and weapons in NETRICSA. Fixed by returning RDTSC.)
- Removed SE1_10.gro because it contains broken textures and breaks the localization of the game. 
  (look the waterfall at the level of the oasis and sierra chiapas). A small SE1_10b.gro is left instead
  containing only the textures of the map for changing the levels of the single player game. 
  The rest of the resources are in the original game files.
- Added variables showing the number of monsters killed, as well as ping for a network game.
  (hud_bShowKills hud_bShowPing).
- Added GetMSLegacyPlayerInf(); function to Entities/Player.es for TFE.
- Added "activemod" to the server response to the request \status\ and \info\.
- Added "difficulty" to the server response to the request \status\ and \rules\.
- Added "location" to the server response to the request \basic\.
  (Note: Now we have full gamespy Implementation of the Query 
  and Reporting without "vipplayers" and "password").
- Removed the day of the week in the strftime() function, 
  as it is incorrectly displayed in the Cyrillic locale.
- Added HUD-Options.cfg and NET-PredictionOptions.cfg in Scripts/CustomOptions.
- Fixed mono sound in MixStereo() funcrioin. Now we have strereo sound in 64-bit mode.
  (look my comments in SoundMixer.cpp and SoundMixer386.asm).
- Fixed broken angle calculation with negative epsilon numbers.
  (see https://github.com/Croteam-official/Serious-Engine/pull/49).
- Fixed loading sequence of tech files in mods.
  (look Engine/Base/Unzip.cpp).
- Fixed Freezing the game when restarting the server at the Hatshepsut level.
  (the bug was in Entities/Lightning.es).

## 2022-02-02 - 2022-02-04
- Added crashfixes for libraries Entities and EntitiesMP from the android port.
  (see https://github.com/Skyrimus/Serious-Sam-Android). 
- Replaced catch char with catch const char. 
- Removed crosshair rendering if the player is dead.

## 2022-05-01 - 2022-05-09
- Fixing sometimes occurring crashes of the game when the player connects to the server.
  (whtn this == null, see Engine/World/World.cpp)
- Added -fno-delete-null-pointer-checks in CMakeLists.txt.
- Added timeout for the connect function when connecting to the master server.
- Added setsockopt for write and read calls when accessing the master server, the socket is switched to non-blocking mode.
- Fixed crash of the game with incorrect cht_iGotoMarker.
- Еngine code excluded from SeriousSam build. Now we have a dynamic libEngine.so library and small SeriousSam,DedicatedServer,MakeFONT files.
  (That's the right thing to do)

## 2022-05-10
- Added amp11lib to project.

## 2022-05-12 - 2022-05-12
- Added Window1251 to Utf8 conversion for SDL_CreateWindow title.
- Added CTString strWindow1251ToUtf8 function.
- Added suport Windows-1251 filenames for game resources.

## 2022-05-20
- Added support Vulkan.

## 2022-05-21
- Added the definition of the Graphical API for SDL_CreateWindow when changing the API via the menu.

## 2022-05-21
- Fixed brightness issues. Thanks to **trs** for the patch.
  https://forum.altlinux.org/index.php?topic=46076.msg369648#msg369648
- Fixed initialization of integer types.
- Update vulkan files from https://github.com/sultim-t/Serious-Engine-Vk

## 2022-05-27
- Update vulkan files from https://github.com/sultim-t/Serious-Engine-RT
- Increased SvkMemoryPool preferredSize for large XPLUS textures.
- some fixes.
- Update files from https://github.com/tx00100xt/SeriousSamClassic

## 2022-05-30 - 2022-06-21
- Fixed insufficient memory for large XPUS textures.
- Fixed wrong Vendor Id.
- Fixed crash game, when trying recovery mode.
- Fixed build for raspberry pi.
- Removing a fixed structure VkPhysicalDeviceFeatures, getting this structure using vkGetPhysicalDeviceFeatures.
- Fixed broken menu and display of models in NETRICSA for platforms not using RDTSC.
- Reverts Critical Section from win32 original code, set multithreading by default.
- Removed check timestrapped for recorded demo.
- Added definition for raspberry pi and e2k.
- Rewrote the game code. Now all user data is stored in the home directory.

## 2022-07-17 - 2022-11-18
- Structuring paths for installation in /usr/bin /usr/lib /usr/share
- Fixed building for RPI4 on 32-bit system.
- Added game data search.
- Fixed timer for gcc 11.3
- Added hud_bShowScore console variable.
- Fixed old scripts for AMD cards.

## 2022-11-30 - 2022-12-20
- Added support Windows.
- Added support FreeBSD.

## 2022-12-22 - 2022-12-30
- Fixed loading of the amp11lib library for the 64-bit version of the game under Windows.
- BSP,Brushes migration from Float3D to Double3D. Now the WorldEditor is working.
- Made the SeriousSkaStudio work.
- Fixed incorrect x64 cpp-implementation of ASM code in lightmap.
- Fixed 64-bit issues in the World Editor. Now the 64-bit version of the World Editor works.
- Fixed levels load from subdirectory (for Windows).

## 2023-01-02
- Fixed macro redefinition in Float.cpp (Windows only bug). 
  (Note: As a result of redefinition, objects inside the world are located incorrectly.
  For Windows, you need to use the definitions from the header which is in the SDK).

## 2023-02-23 - 2022-03-25
- Fixing a bug with thunder, the sound of thunder and flashes on the level of Hatshepsut.
- Fixed loading libvorbisfile library for non-source-based distros.
- Fixed bug with ioctlwbufget.
- Added portable mode for command line (+portable). In portable mode, all user data is stored in the game directory.
