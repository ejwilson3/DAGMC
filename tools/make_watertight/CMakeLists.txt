message(STATUS "Building make_watertight")

# Source files
set(SRC_FILES)
list(APPEND SRC_FILES gen.cpp)
list(APPEND SRC_FILES arc.cpp)
list(APPEND SRC_FILES zip.cpp)
list(APPEND SRC_FILES cleanup.cpp)
list(APPEND SRC_FILES mw_func.cpp)
list(APPEND SRC_FILES cw_func.cpp)

# Public headers
set(PUB_HEADERS)
list(APPEND PUB_HEADERS gen.hpp)
list(APPEND PUB_HEADERS arc.hpp)
list(APPEND PUB_HEADERS zip.hpp)
list(APPEND PUB_HEADERS cleanup.hpp)
list(APPEND PUB_HEADERS cw_func.hpp)
list(APPEND PUB_HEADERS mw_func.hpp)

# Libraries
set(LINK_LIBS)
list(APPEND LINK_LIBS ${DAG_LINK_LIBS})

# Define executables
add_executable(make_watertight make_watertight.cpp ${SRC_FILES})
add_executable(check_watertight check_watertight.cpp ${SRC_FILES})

# Include directories
include_directories(.)
include_directories(${MOAB_INCLUDE_DIRS})

# Link executables to moab/dagmc libraries
target_link_libraries(make_watertight ${LINK_LIBS})
target_link_libraries(check_watertight ${LINK_LIBS})

# Install
install(TARGETS check_watertight make_watertight DESTINATION ${INSTALL_BIN_DIR} PERMISSIONS ${PERMS})

# build tests
add_subdirectory(tests)