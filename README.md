# UIAutomation DLL Helper - Allows Delphi 13 Apps to Work on Windows XP, Windows 2003, and ReactOS

![GitHub Release](https://img.shields.io/github/v/release/JohnTHaller/UIAutomation-DLL-Helper)
![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/JohnTHaller/UIAutomation-DLL-Helper/total)
![GitHub License](https://img.shields.io/github/license/JohnTHaller/UIAutomation-DLL-Helper)
![GitHub Repo stars](https://img.shields.io/github/stars/JohnTHaller/UIAutomation-DLL-Helper)

Dependency on UIAutomation.dll is compiled by default into executables produced by Delphi 13 as well as some other compilers. Windows XP and Windows 2003 won't have this DLL available in system32 unless .NET 3.5 is installed. ReactOS won't have this DLL available and .NET 3.5 can't be installed onto it. Without the DLL present, the Delphi executable will fail to run and the app will not work, even after manually changing the PE Header version in Linking to allow the executable to run on legacy Windows. (see below for details)

I've created a basic UIAutomation.dll using [Dummy DLL Generator](https://github.com/ykhwong/dummy-dll-generator), adjusted the appropriate manifest details, and digitally signed it using the same Rare Ideas, LLC code signing certificate used by [PortableApps.com](https://portableapps.com/). This dll can be placed alongside your Delphi executable to allow it to work on Windows XP, Windows 2003, and ReactOS even without the .NET 3.5 installed.

## To Install

1. Download the UIAutomation.dll file from the [Releases section](https://github.com/JohnTHaller/UIAutomation-DLL-Helper/releases)
2. Place the DLL in the same directory as your Delphi executable set with the proper PE headers (below)
3. Profit!

## Known Issues / Bugs

With this workaround in place, executing a TOpenDialog will cause the app to crash on some Windows 10 PCs (and possibly other machines as a specific reason has not been determined). I recommend only including the UIAutomation.dll file on Windows XP systems.

## Setting The PE Header in Delphi 13 For Compatibility With Legacy Windows

To set the PE version in Delphi 13 of a given project, click Project from the main menu, then select Options, expand Building, expand Delphi Compiler, expand Linking, then adjust the fields "Set OS Versdion fields in PE Header as..." and "Set Subsystem Version fields in PE Header as..." to 5.1. If you use System.Threading, you'll need to [tweak GetTickCount](https://en.delphipraxis.net/topic/5536-delphi-11-windows-xp-compatibility-tweak/).

## License

The DLL is licensed under the MIT license for compatibility with any release you'd like to use it with.
