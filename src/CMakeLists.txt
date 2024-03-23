add_executable(default_cpp main.cpp)


if(CMAKE_COMPILER_IS_GNUCXX)
  target_link_libraries(default_cpp gomp m stdc++fs)
endif()
set_target_properties(default_cpp PROPERTIES CXX_STANDARD 20)