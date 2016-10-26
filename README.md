CMakeDLLDemo
==========================

CMake example inspired by [this](http://cognitivewaves.wordpress.com/cmake-and-visual-studio/) tutorial for Visual Studio.

### Installation

Create a build directory and call cmake from the command line, indicating where the CMakeLists.txt file is:

	CMakeTest\build> cmake ../src -G "Visual Studio 14 2015 Win64"

Change the target build environment as appropriate.

Open the solution file in Visual Studio, and build the ALL_BUILD project.

### Initial Configuration (Visual Studio)

Before this will run in Visual Studio, fix the following glitches:

1) By default, ALL_BUILD will be the startup project. Right click on the app project and click `Set as Startup Project`.

2) The app.exe executable depends on the math.dll that we built with ALL_BUILD, but the system doesn't know how to find it. Build the INSTALL project. This will copy app.exe and math.dll to the bin directory in the build folder.

3) Running app.exe through Visual Studio still won't work, because the command is referencing the copy of app.exe in the `app/Debug` folder, rather than the new copy in the bin directory. Right click on the app project, and select Properties -> Debugging. Set the command to `..\bin\app.exe` and set Command Arguments to some number (e.g. 200).

Now, when you tell Visual Studio to call app.exe, it is able to find math.dll, because there is a copy of it in the same folder.

### Debugging

Be sure to re-run INSTALL after each build. Otherwise, when you run through the IDE, you would be running the previous version of the code in the bin directory, and you will not be able to see the effects of your changes.