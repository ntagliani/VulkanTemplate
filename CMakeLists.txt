cmake_minimum_required(VERSION 3.23)

project(VulkanTemplate LANGUAGES CXX)

message("Building with CMake version: ${CMAKE_VERSION}")

find_package(glfw3 REQUIRED)
find_package(volk REQUIRED)
find_package(VulkanHeaders REQUIRED)
find_package(glm REQUIRED)
find_package(VulkanLoader REQUIRED)

set(SOURCES
    src/main.cpp
)

add_executable(${PROJECT_NAME} ${SOURCES})

target_link_libraries(${PROJECT_NAME} PRIVATE glfw Vulkan::Loader volk::volk vulkan-headers::vulkan-headers glm::glm)