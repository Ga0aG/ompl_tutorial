cmake_minimum_required(VERSION 3.10.2)
project(ompl_tutorial)

find_package(ompl REQUIRED)
find_package(ament_cmake REQUIRED)

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
    add_compile_options(-Wno-overloaded-virtual)
endif()

include_directories(SYSTEM
                    ${Boost_INCLUDE_DIRS}
                    ${OMPL_INCLUDE_DIRS})

add_executable(rigid_body_planning src/RigidBodyPlanning.cpp)

# target_include_directories(${PROJECT_NAME}
#   PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
#   PUBLIC $<INSTALL_INTERFACE:include>
# )
target_include_directories(rigid_body_planning PUBLIC ${OMPL_INCLUDE_DIRS})
target_link_libraries(rigid_body_planning PUBLIC ${OMPL_LIBRARIES})

# Install executables
install(TARGETS
  rigid_body_planning DESTINATION lib/${PROJECT_NAME}
)

ament_package()
