# UE4-NetworkingSetup2016
A guide that takes the old tutorials found online and gives everything beginners need to know to setting up a server for linux / windows.

Guide made using UE4 4.10 and this computer to build/package: http://www.amazon.com/Alienware-Aurora-R3-Gaming-Machine-Overclocked/dp/B006L9QBQ6

And tested using the default "Vehicle Advanced" code example. (The simple one with orange ramps). DO NOT HAVE "game" of any capitalization in your project name. Trust me on this.

BEFORE CONTINUING: Make sure you've set up your VS for UE4:
https://docs.unrealengine.com/latest/INT/Programming/Development/VisualStudioSetup/index.html#beforesetting-upyourue4-to-vsworkflow

Using these steps as reference, this file documents what did and did not work getting the server to work.

#NOTE: Read several steps ahead of the step you're actually on. Making sure this can build a windows server first is always easier. If it can build windows, it can build for linux.

The following links were used as reference:
DG -- https://wiki.unrealengine.com/Dedicated_Server_Guide_(Windows_%26_Linux)
SS -- https://wiki.unrealengine.com/Standalone_Dedicated_Server
(In this guide, the above will be refferred to as either DG or SS)

1. Getting the engine compiled and running was actually fairly straightforward. DG has the link to building your very own engine. MAKE SURE TO CHECKOUT THE PROPER BRANCH FOR YOUR VERSION. 
Note: I didn't install the "Git for Windows" crap. If you're using a GUI (and not terminal) then you should feel bad.
Time to do: Several Hours.

2. Make sure to also have UnrealBuildTool, UnrealFrontend, UnrealHeaderTool and UnrealLightmass built. These are found under the Programs folder next to the Engine folder in your Solution Explorer in VS.

3. From here, you can launch the editor from C:\Users\<MyUsername>\Documents\UnrealEngine\Engine\Binaries\Win64 but step 3 of DG is better if you already have a project you want to compile. 

--The following is for if you want to run your server on a LinuxOS (recommended). IF you're running off a windows computer, skip to step 6 --
4. We need to do to some setup to properly compile on linux. So let's get started. On DG go directly to step 1 of the Linux half. So I did not have system admin rights for this but still managed to do it and step 1 is about getting your path to CLANG correct. This should be fairly trivial. First get the download that you find in DG's Step 1 instructions, and then run the Setup.bat file. It'll generate a "OutputEnvVars.txt" that'll give you the proper path. The command that worked for me was 
"[Environment]::SetEnvironmentVariable("LINUX_ROOT", "C:\Users\eliot2\Downloads\v3_clang-3.3_ld-2.24_
glibc-2.12.2\toolchain", "User") "

5. I didn't do DG's Linux Step 2. You can if you want, didn't matter for me. 

6. Return back to SS. What you want from here is that "Server Target" code. Follow the instructions from the "Compilation" in bold, down to "Open Visual Studio, set the configuration to *Server and select the platform target accordingly." Note: DO NOT MAKE A NEW FILE VIA VISUAL STUDIO. It'll take forever scanning literally 40 thousand header files just to make a "generic C++ class". Just Copy and paste into a notepad .cs file what you need and put it into the folder they tell you to in the SS page. Close VS and make sure to run the "GenerateProjectFiles.bat" and the "Setup.bat" in the UnrealEngine folder. Then right click your game's *.uproject file and choose "Generate Visual Studio Project Files". Make sure to reload VS to have your file appear. 

7. From here it's simple and straightforward compiling and building. The server programs reference files outside of themselves, despite the fact they're packaged. So you use the editor to package a non-server executable, then put the server executable next to the non-server one and it works. This applies to both linux AND windows. Step 2 of Linux of DG actually works for windows as well, and it's easier than learning UE Frontend's nuances unless you're planning on using the frontend for bulk patching and testing.

If you have any questions or constructive criticism please email me at eliot@kitelion.me

