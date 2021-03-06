- Note the directory where Aria was installed (usually, C:/Program Files/MobileRobots).
- Open MobileSim, and load the map you’ve downloaded. Keep this program open.
- Open CLion
- (If you try and ‘Build’ this solution, then you’ll get two errors saying that it ‘Cannot open include file: ‘Aria.h’’)
- What we’re doing here is to find and link the Aria files to the project.
- Go to CMakeLists.txt

Based on Visual Studio setup I had the following:
```
C++ -> General -> Additional Include directories:

C:\Program Files\MobileRobots\Aria
C:\Program Files\MobileRobots\Aria\include
C:\Program Files\MobileRobots\Aria\bin64
C:\Program Files\MobileRobots\Aria\lib64


Linker -> General -> Additional library directories: 

C:\Program Files\MobileRobots\Aria\lib64

Linker -> Input -> Additional dependencies:

AriaDebugVC14.lib
```


target_link_libraries() ??? to do the below?


- Select ‘VC++ Directories’ under ‘Configuration Properties’.
- Next, you’ll see the following list:
  - Executable Directories
  - Include Directories
  - …
  - Exclude Directories
- Note that for 4 items, the contents are in bold, meaning these are linked folders.
- For each of these bold items, click on the ‘Down Arrow box’ when you select a line, then select ‘<Edit…>
- For the popup window, you’ll see a value that links to ‘C:\Program Files\SA\MobileRobots\Aria…’ for the following list, change the file path to the path of your Aria installation, leaving the last folder value.
  - For example, So ‘C:\Program Files\SA\MobileRobots\Aria\bin64’ should now be So ‘C:\Program Files\MobileRobots\Aria\bin64’
- Do this for:
  - Executable Directories
  - Include Directories
  - Library Directories
  - Source Directories
- Once that’s done, click OK and close all the properties windows.
- Right click the project and ‘Build’ the solutions.
- If no errors appear, run the solutions with ‘Local Windows Debugger’
- The program should run and show the robot moving in the simulator!


https://marketplace.visualstudio.com/items?itemName=DaisukeAtaraxiA.VSslnToCMakePlugin


## Current state:

Now in the file `FindARIA.cmake` do the below:

ok, so that find module will define the following variables ARIA_FOUND, ARIA_INCLUDE_DIRS, ARIA_LIBRARIES
it's an old style module, you'll have to manually call target_include_directories for include dirs, and target_link_libraries for libs

so basically add similar directories to this file, as though I did above for visual studio project ARIA, and for the visual studio project ARIA itself.

 yeah, as suspected, the find package command finds the library, you are just not doing anything with the variables it sets
 
  ok, so that find module will define the following variables ARIA_FOUND, ARIA_INCLUDE_DIRS, ARIA_LIBRARIES
  
  Update `FindARIA.cmake` file to the following dynamics:
  
  https://cmake.org/cmake/help/latest/command/target_include_directories.html
  
  https://cmake.org/cmake/help/latest/command/target_link_libraries.html
  
  target_include_directories(yourexecutabletarget ${ARIA_INCLUDE_DIRS})
  target_link_libraries(yourexecutabletarget ${ARIA_LIBRARIES})
  
  arguments are the expressions you pass a command to initialize its parameters
  `CLion` and `${ARIA_INCLUDE_DIRS}` are the arguments given to `target_include_directories`
   the docs for the command, specifying how many params it expects and where https://cmake.org/cmake/help/latest/command/target_include_directories.html
   as per above docs I need to set `<INTERFACE|PUBLIC|PRIVATE>` somehow for 
   
   `target_include_directories(CLion ${ARIA_INCLUDE_DIRS})`
   
   `target_link_libraries(CLion ${ARIA_LIBRARIES})`
   
   In conclusion I believe this version of ARIA that is in this repo, as in the setup files for windows and libraries for ARIA are all compiled towards the microsoft visual studio compiler,
   this means that to run Aria using this CMake setup in Windows, in the CLion IDE or similar, I would need to recompile for its appropiate set compiler which in my case is GCC (https://nuwen.net/mingw.html)
   Aria can be compiled from source for GCC for windows possibly from: https://github.com/reedhedges/AriaCoda