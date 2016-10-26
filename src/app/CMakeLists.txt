# Write information to the console.
message("Running CMakeLists.txt for app...")

# Create app.exe from main.cxx. Equivalent to setting
# Properties -> General -> Configuration Type to Application(.exe)
add_executable(app main.cxx)

# Add the search directory for the math library header files. This is equivalent
# to Properties -> C/C++ -> General -> Additional Include Directories.
include_directories("${PROJECT_SOURCE_DIR}/math")

# Add the math library as a dependency. Equivalent to
# Properties -> Linker -> Input -> Additional Dependencies
target_link_libraries(app math)

# Create a solution folder called "executables" and add the main project (app) to it.
# (This doesn't seem to do anything in Eclipse.)
set_property(TARGET app PROPERTY FOLDER "executables")

# Adds logic to INSTALL.vcproj to copy MyApp.exe to the install directory.
install(TARGETS app RUNTIME DESTINATION ${PROJECT_BINARY_DIR}/bin)
