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
