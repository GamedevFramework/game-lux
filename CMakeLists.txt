cmake_minimum_required(VERSION 3.10)

project(LUX
  VERSION 0.1.0
)

include(GNUInstallDirs)

find_package(gf REQUIRED COMPONENTS graphics)

set(LUX_DATA_DIR "${CMAKE_INSTALL_PREFIX}/share/games/lux")
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/code/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h @ONLY)

add_executable(lux
  code/lux.cc
  code/local/Bonus.cc
  code/local/Bullets.cc
  code/local/Enemy.cc
  code/local/Hero.cc
  code/local/Particles.cc
  code/local/Scenario.cc
  code/local/Ship.cc
  code/local/Shoot.cc
  code/local/Stars.cc
)

target_include_directories(lux
  PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/code
    ${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(lux
  PRIVATE
    gf::graphics
)

install(
  TARGETS lux
  RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
)

install(
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/data/lux"
  DESTINATION "${CMAKE_INSTALL_DATAROOTDIR}/games"
)
