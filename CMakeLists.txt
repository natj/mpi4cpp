cmake_minimum_required (VERSION 3.5)

set (CMAKE_CXX_STANDARD 17)
set (CMAKE_CXX_STANDARD_REQUIRED ON)
set (CMAKE_CXX_EXTENSIONS OFF)

project (mpi4cpp)

# set location of libraries
set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/lib)



##################################################
# dependencies

# fmt preinstallation fails with intel compilers
#FIND_PACKAGE (FMT REQUIRED)
#INCLUDE_DIRECTORIES ( "$ENV{FMT_INCLUDE_DIR}" )


# hpc stuff 
find_package (MPI)



##################################################
# targets build

#-------------------------------------------------- 
# Warning flags based on the compiler
set (WARNING_FLAGS
    $<$<CXX_COMPILER_ID:GNU>:
        -Wall -Wextra -Wpedantic
    >
    $<$<CXX_COMPILER_ID:Clang>:
        -Wall -Wextra -Wpedantic -Wno-missing-braces -g
    >
)

#-------------------------------------------------- 

include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/include )
include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/tools/optional-lite/include )


enable_testing()
#add_subdirectory(test EXCLUDE_FROM_ALL)
add_subdirectory(test)


