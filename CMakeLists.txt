cmake_minimum_required(VERSION 3.5)

project(ros_gz_lehrforst_sim)

find_package(ament_cmake REQUIRED)

set(ROBOTS
  bunker
  scout
  scout_bumper
)

install(
  DIRECTORY
    config/
  DESTINATION share/${PROJECT_NAME}/config
)

install(
  DIRECTORY
    launch/
  DESTINATION share/${PROJECT_NAME}/launch
)

install(
  DIRECTORY
    models/
  DESTINATION share/${PROJECT_NAME}/models
)

install(
  DIRECTORY
    worlds/
  DESTINATION share/${PROJECT_NAME}/worlds
)

foreach(robot ${ROBOTS})
  set(xacro_file
    "${CMAKE_CURRENT_SOURCE_DIR}/models/${robot}/model.xacro"
  )
  set(sdf_file
    "${CMAKE_INSTALL_PREFIX}/share/${PROJECT_NAME}/models/${robot}/model.sdf"
  )
  execute_process(
      COMMAND xacro ${xacro_file} -o ${sdf_file}
      RESULT_VARIABLE XACRO_RESULT
  )
endforeach()

ament_package()
