This works for the GOG versions of BG1EE and BG2EE
This is generally for an EET install. My brother and I spent quite a bit
of time figuring all this stuff out. There were some useful guides, but
not every problem we ran into had a posted solution; at least that we could find.
I hope this will fill that need, and help someone else save a bit of time!


WeiDu Tool Installation
There is a good write up for this at:
https://moebiusproject.gitlab.io/mods_on_linux
The following is an abridged version of Step 1 of that guide

1. Download weidu tool
https://github.com/WeiDUorg/weidu/releases

2. Move weidu tool to appropriate directory and extract the archive; I used
~/.local/bin/bgModTools/WeiDU-Linux/

3. export to $PATH
export PATH=~/.local/bin/bgModTools/WeiDU-Linux/

4. test with weidu --help or weidu --version



Game and Mod Installation
1. Create winetricks prefix in appropriate directory. I used
export WINEPREFIX=~/baldursGateWin

2. Use the game installation scripts; must be installed at least 1 level inside drive_c/
During installation I specified the top level game directories as BaldursGateEnhancedEdition
and BaldursGateIIEnhancedEdition

3. Copy x86_64 directory with libssl files into directory above game/
~/baldursGateWin/drive_c/baldursGate/BaldursGateIIEnhancedEdition/x86_64
These can be downloaded from:
https://github.com/xanathar/baldursgate_ee_libssl_files

4. Edit start.sh script (located above game/); append after "source support/gog_com.shlib"
export LD_LIBRARY_PATH="$CURRENT_DIR/x86_64/"

5. Enable casefolding on the following directories:
BaldursGateEnhancedEdition, BaldursGateIIEnhancedEdition (the top level directory for each installation),
Also these directories for EACH installation: game, lang, and certain mod directories as needed
Directories must be empty to enable casefolding
to do this easily cd to inside the directory and run the following commands (or do it through the GUI):

mkdir temp
mv * temp/
mv temp/ ..
cd ..
chattr +F folderName
mv temp/ folderName/
cd folderName/temp/
mv * ..
cd ..
rm temp/
(there is probably a faster and more efficient way to do all this, but this is what I did)
This needs to be done for EACH directory that requires casefolding

6. Make lower case symlink to home directory if needed (likely needed for EET installs)
_hdir="~"; sudo ln -s ~ ${_hdir,,}

Repeat for each mod:
7. Extract mod archives; enable casefolding on mod folders if needed

8. Move directory containing .tp2 file to game/ if needed

9. Run weidu installer on the mod
weinstall modName



General Mod Order Guidelines
Current mod compatibility list:
https://k4thos.github.io/EET-Compatibility-List/EET-Compatibility-List.html#native
Check this page to see which mods need to be installed before EET, and are otherwise
compatible with it. Note, these will work for EET, but may still conflict with each other.
Read the readme's!

Check readme files for each mod for specifics, but generally the following order is recommended:

Top
1.DlcMerger (needed in BGEE regardless of EET IF SoD is installed)
2. * Fix mods required before EET (EE Fixpack)
3. * Atypical mods required before EET
4. * Item mods required before EET
5. * Store mods required before EET
6. * Quest / content mods required before EET (bg1 unfinished business for example)
7. * NPC mods required before EET
8. EET
9. + Eeex
10. Atypical mods (portraits, audio)
11. Item mods
12. Store mods
13. Quest / content mods
14. NPC mods
15. Tweak / tactical mods
16. EET_end
Bottom

 * check the compatibility list to see which of these mods need to be installed before EET

 + As far as I'm aware this an only be used on WINDOWS installation of BG1, BG2, or EET
 + and cannot be used on the native linux version
 + Must be installed before other mods relying on script extender, but can actually be installed anywhere

Within each category it is good practice to order mods from oldest to newest

This is just a general guideline for install order; exceptions exist.
