cmake_minimum_required(VERSION 3.5)

project(ros_gz_lehrforst_sim)

find_package(ament_cmake REQUIRED)

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

ament_package()


set(ROBOTS
  bunker
  scout
  scout_bumper
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


set(GEN_TREE_SCRIPT
  "${CMAKE_CURRENT_SOURCE_DIR}/models/lehrforst_trees/generate_lehrforst_trees_model_sdf.py"
)
set(GEN_TREE_TARGET
    "${CMAKE_INSTALL_PREFIX}/share/${PROJECT_NAME}/models/lehrforst_trees"
)
file(MAKE_DIRECTORY ${GEN_TREE_TARGET})
execute_process(
    COMMAND python3 ${GEN_TREE_SCRIPT} ${GEN_TREE_TARGET}
    RESULT_VARIABLE GENERATE_TREES_RESULT
)
