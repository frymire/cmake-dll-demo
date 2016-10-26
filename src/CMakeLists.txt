cmake_minimum_required (VERSION 2.6)

# Write information to the console.
message("Running CMakeLists.txt for CMakeDLLDemo...")

# Maps to a solution file (Tutorial.sln). The solution will 
# have all targets (exe, lib, dll) as projects (.vcproj)
project(CMakeDLLDemo)

# Turn on the ability to create folders to organize projects.
# By default, it creates the "CMakePredefinedTargets" folder to 
# store the ALL_BUILD, INSTALL, RUN_TESTS, and ZERO_CHECK projects.
# (This doesn't seem to do anything in Eclipse.)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

# You can set compiler flags like this.
# set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")

# Add sub-directories where more CMakeLists.txt exist.
add_subdirectory(app)
add_subdirectory(math)

# Turn on CMake testing capabilities
enable_testing()
add_test(AppTest100 ${PROJECT_BINARY_DIR}/bin/app.exe 100)
add_test(AppTest200 ${PROJECT_BINARY_DIR}/bin/app.exe 200)
add_test(AppTest300 ${PROJECT_BINARY_DIR}/bin/app.exe 300)
