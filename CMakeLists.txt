cmake_minimum_required(VERSION 2.6)
set(CMAKE_C_COMPILER "/usr/local/Cellar/llvm/9.0.0/bin/clang")
set(CMAKE_CXX_COMPILER "/usr/local/Cellar/llvm/9.0.0/bin/clang++")

project (mih)

find_library (HDF5_LIB hdf5 "/usr/local/include/")

set (CMAKE_CXX_FLAGS "-DSINGLE_CORE -O2 -fopenmp -DNDEBUG -Wno-c++11-narrowing")
# -Wall -march=native -mtune=native")

include_directories ("${PROJECT_SOURCE_DIR}/include")

add_executable (mih src/array32.cpp src/mihasher.cpp src/sparse_hashtable.cpp src/bucket_group.cpp interface/mih_interface.cpp src/reorder.cpp interface/loadVar.cpp interface/saveRes.cpp)
target_link_libraries (mih ${HDF5_LIB})

project (linscan)
add_executable (linscan interface/linscan_interface.cpp src/linscan.cpp interface/loadVar.cpp interface/saveRes.cpp)
target_link_libraries (linscan ${HDF5_LIB})
