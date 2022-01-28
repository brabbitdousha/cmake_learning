``` cpp
# 1. Requirements
cmake_minimum_required(VERSION 2.8.11)
project(stl_iteration)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 2.Configuration
#add_compile_options(-Wno-deprecated)  # This is just to avoid some spammy warnings
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)  # This line is optional. It's just for certain IDEs to use

# 3. Boilerplate
#usd
set(USD_LIBRARY_DIRECTORY D:/UGit/x/out5/third_party/USD/usd_lib)
set(USD_INCLUDE_DIRECTORY F:/USD/build6/include)
#boost
set(BOOST_INCLUDE_DIRECTORY E:/install/boost/include/boost-1_70)
set(BOOST_PYTHON_LIBRARY_DIRECTORY E:/install/boost/lib)
#tbb
set(TBB_LIBRARY_DIRECTORY E:/install/oneTBB-tbb_2018/lib)
set(TBB_INCLUDE_DIRECTORY E:/install/oneTBB-tbb_2018/include)

#boost
find_library(USD_BOOST_PYTHON boost_python39-vc142-mt-gd-x64-1_70 HINTS ${BOOST_PYTHON_LIBRARY_DIRECTORY})
#usd stuff
find_library(USD_KIND usd_kind HINTS ${USD_LIBRARY_DIRECTORY})
find_library(USD_SDF usd_sdf HINTS ${USD_LIBRARY_DIRECTORY})
find_library(USD_TF usd_tf HINTS ${USD_LIBRARY_DIRECTORY})
find_library(USD_USD usd_usd HINTS ${USD_LIBRARY_DIRECTORY})
find_library(USD_USDGEOM usd_usdGeom HINTS ${USD_LIBRARY_DIRECTORY})
#tbb
find_library(USD_TBB NAMES tbb_debug HINTS ${TBB_LIBRARY_DIRECTORY})

find_package(PythonLibs REQUIRED)

# 4. Include/Link Everything
add_executable(run_it
	main.cpp
)

target_include_directories(run_it
PUBLIC
	${PYTHON_INCLUDE_PATH}
	${USD_INCLUDE_DIRECTORY} 
    ${BOOST_INCLUDE_DIRECTORY}
	${TBB_INCLUDE_DIRECTORY}

)

target_link_directories(run_it
PUBLIC 
    ${USD_LIBRARY_DIRECTORY}
	${BOOST_PYTHON_LIBRARY_DIRECTORY}
)

target_link_libraries(
run_it
	${PYTHON_LIBRARY}
	${USD_TBB}
	${USD_BOOST_PYTHON}
	${USD_SDF}
	${USD_TF}
	${USD_USDGEOM}
	${USD_USD}
    ${USD_KIND}
)
Add_Definitions(-DNOMINMAX)
set(MY_PATH "PATH=${USD_LIBRARY_DIRECTORY};%PATH%" ${MY_CUSTOM_PATH})
set_target_properties(run_it PROPERTIES VS_DEBUGGER_ENVIRONMENT "${MY_PATH}")
```