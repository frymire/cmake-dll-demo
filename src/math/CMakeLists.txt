# Write information to the console.
message("Running CMakeLists.txt for math...")

# Collect sources into CMake variables. You can use regular expressions, but CMake 
# recommends explicitly listing each source. We'll do that for the advanced subfolder.
file(GLOB MATH_HEADERS "*.h")
file(GLOB SIMPLE_SOURCES "simple/*.h" "simple/*.cxx")
set(ADVANCED_SOURCES "advanced/AdvancedFunctions.h" "advanced/AdvancedFunctions.cxx")

# If we just add those collected sources to the project, the folder structure will be
# lost, so we add those back explicitly. The empty stores files at the project level.
source_group("" FILES ${MATH_HEADERS})
source_group("simple" FILES ${SIMPLE_SOURCES})
source_group("advanced" FILES ${ADVANCED_SOURCES})

# Include this folder as a search directory for headers. Equivalent to
# Properties -> C/C++ -> General -> Additional Include Directories
include_directories(.)

# Create math.dll with the listed sources collected in the variables. Equivalent to 
# setting Properties -> General -> Configuration Type to Dynamic Library(.dll)
add_library(math SHARED ${MATH_HEADERS} ${SIMPLE_SOURCES} ${ADVANCED_SOURCES})

# Create a folder "libraries" and adds target project (math.vcproj) under it
# (This doesn't seem to do anything in Eclipse.)
set_property(TARGET math PROPERTY FOLDER "libraries")

# Add logic to the INSTALL project to copy math.dll to the destination directory.
install(
	TARGETS math
	RUNTIME DESTINATION ${PROJECT_BINARY_DIR}/bin
	LIBRARY DESTINATION ${PROJECT_BINARY_DIR}/bin
)
