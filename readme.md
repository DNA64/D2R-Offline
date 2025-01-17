# Diablo II Resurrected - Offline Patcher

A simple tool that remaps & bypasses *Diablo II Resurrected* module and then continues to patch connection functions to allow local gameplay. 

# Setup

## Getting Started

With the Technical Alpha and Beta now over, the installation files available on blizzards servers have now been encrypted, making it pointless to download them directly from the Battle.net servers. For legal reasons this means you'll have to find the files on your own if you don't already have them. Once you have found the files, you can proceed with the guide.

## Installing

1. You will need the *Diablo II Resurrected* game files, as mentioned above.

1. You may also need [.NET Framework v4.7.2](https://dotnet.microsoft.com/download/dotnet-framework/thank-you/net472-web-installer).

1. Download the latest release *(or clone the project and build it)* :  
https://github.com/ferib/D2R-Offline/releases  
Unzip and copy **both** `D2ROffline.exe` and `patches.txt` to your *Diablo II Resurrected* game folder. They should be in the same directory as `Game.exe`.

## Running

1. Double-click `D2ROffline.exe` to start the tool.

1. A cmd window should open and begin the patching process.

1. Done!


When loading a character, double clicking the character name or clicking Play will not work by default. See the `-FixLocalSave` argument under [Usage](#Usage) if you would like to edit your saves to play in offline mode *(including act1 to act5)*.

> _NOTE: You may need to run this tool **twice** for it to work properly. If after the first try it does not load your save games in offline mode, close the game and run `D2ROffline.exe` again._

## Please see the [FAQ](FAQ.md) if you have any issues.

# Usage

## Arguments
You can run `D2ROffline.exe` with arguments to solve some problems. Try launching with arguments by using a [batch script](#Bash).

### -FixLocalSave
`.\D2ROffline.exe -FixLocalSave` This will update your save files to allow you to play your characters in single-player mode *(act3 to act5 included)* instead of hosting a TCP/IP game. This argument prevents the game from loading and will just patch your save files. **Please note that this will also unlock all quests so that you can jump right into all acts.**

### -w
`.\D2ROffline.exe -w` Launch the game in Windowed Mode.

### -txt -direct
`.\D2ROffline.exe -txt -direct` Allows you to use modified txt files (Example: `E:\D2R\Data\global\excel\treasureclassex.txt`) extracted from the game using [CascView](https://www.hiveworkshop.com/threads/ladiks-casc-viewer.331540/). 

### -FixLocalSaveNoQuests
`.\D2ROffline.exe -FixLocalSaveNoQuests` Does the same as `-FixLocalSave` but without unlocking any quests.

### -FixLocalSaveResetQuests
`.\D2ROffline.exe -FixLocalSaveResetQuests` In case you used `-FixLocalSave` by mistake and now you want to reset the quests back to normal.

### -UpdateKeyBinds
`.\D2ROffline.exe -UpdateKeyBinds` This will sync your keybindings between characters using custom`.key` files.

### -Delay \<delay in ms>
`.\D2ROffline.exe C:\D2R\Game.exe -Delay 35` This will change the delay amount when patching your game, default is 25. Use this and try different values to help with crashes after being in-game for certain amounts of time.

### "Game.exe file path"
`.\D2ROffline.exe C:\D2R\Game.exe` Use this to specify a path to Game.exe if you're not running `D2ROffline.exe` from the same directory.

### Passing arguments
`.\D2ROffline C:\D2R\Game.exe -txt -direct -w` The patcher will pass all other arguments, which are in our case `-txt -direct -w`, to the game so that you can launch them as you wish.

## Custom Patches

There is a neat little feature that allows you to use the `patches.txt` file and create your own patching rules, the `patches.txt` file **MUST** be in the same folder as the executable!
This allows you to create your own patches.

## Patches

Offline/Local patch, thanks to [king48488](https://www.ownedcore.com/forums/diablo-2-resurrected/diablo-2-resurrected-bots-programs/940315-some-basic-offsets-let-you-play-offline.html)
```
0xD4AD68:9090
0xD4E25F:909090909090
0xCAFB9D:90B001
0x597E1C:90909090909090
```

All classes, Multiplayer access and unlock act3~5 thanks to [shalzuth]()
```
0xD615F2:909090909090909090909090909090909090909090909090909090: ~ show all calsses on load (shalzuth)
0x39FC03:9090909090909090909090909090909090909090: ~ allow chars to load (shalzuth)
0x39FCB6:909090909090909090: ~ enable loading into a3-a5 (shalzuth)
```

Language patches to force the client into loading a language, thanks to Ferib (me).
```
0x1446C8:+0x00: ~ English *[enUS]*
0x1446C8:+0x270A4: ~ German *[deDE]*
0x1446C8:+0x270AC: ~ Spanish *[esES]*
0x1446C8:+0x270B4: ~ French *[frFR]*
0x1446C8:+0x270BC: ~ Italian *[itIT]*
0x1446C8:+0x270C4: ~ Korean *[koKR]*
0x1446C8:+0x270CC: ~ Polski *[plPL]*
0x1446C8:+0x270D4: ~ Russian *[ruRU]*
0x1446C8:+0x270DC: ~ Chinese (simplified) *[zhCN]*
0x1446C8:+0x270E4: ~ Chinese *[zhTW]*
0x1446C8:+0x270EC: ~ Spanish *[esMX]*
0x1446C8:+0x270F4: ~ Japanese *[jaJP]*
0x1446C8:+0x270FC: ~ Brazilian *[ptBR]*
```

## How To: Connect via TCP/IP

The host must login to their router's configuration interface (usually 192.168.1.254 or 192.168.0.254 or try changing `254` to `1`) and forward TCP port 4000 to their internal IP.  The host can find the internal IP address by using the command `ipconfig` from a CMD window.
    
Any Player(s) wanting to connect to the host then simply enter the host's external IP in the game's interface. 
The host can find this IP address by visiting whatsmyip.org or running `ipconfig` again.

 **The shared stash does not work for TCP/IP games.**  Back up your shared stash  **before**  playing TCP/IP, and do not put items in the stash during TCP/IP games, all items in shared stash will be lost.

# Bash

Copy and Paste the bash script below into Notepad and save the file to your desktop as something like `D2R-Offline.bat`. Launch the game using this file.

```
@ECHO OFF
E:
cd "D2R Alpha"
.\D2ROffline.exe "E:\D2R\Game.exe" -txt -direct -delay 300
```

> _NOTE: The above patches are modifying the .text section of the game, for those that want to patch the .data section you can simply use Cheat Engine because the anti-cheating does not scan those areas for modified values._

# Notices
This repository is for educational purposes only. 
Please do not perform any of the above actions on the Game client.

Diablo II and Diablo II: Resurrected are registered trademarks of Blizzard Entertainment. 
This project is not affiliated with Blizzard Entertainment in any way.


# Credits
 - Ferib : [crc32 bypass](https://ferib.dev/blog.php?l=post/Bypassing_World_of_Warcraft_Crc32_Integrity_Checks)
 - king48488: [Patch locations](https://www.ownedcore.com/forums/diablo-2-resurrected/diablo-2-resurrected-bots-programs/940315-some-basic-offsets-let-you-play-offline.html)
