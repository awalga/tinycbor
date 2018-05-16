################################
## Cmake dependencies
################################

include(GNUInstallDirs)
################################
## Compiler Flags
################################

################################
## Dependencies
################################

################################
# Build Tools
################################
add_executable(cbordump cbordump/cbordump.c)
target_include_directories(cbordump
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
        PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
        $<INSTALL_INTERFACE:include)
target_link_libraries(cbordump tinycbor)

################################
## Install Tools
################################
install(TARGETS cbordump RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})