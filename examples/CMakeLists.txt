add_executable(list_ports list_ports.c)
target_link_libraries(list_ports ${PROJECT_NAME})

add_executable(port_info port_info.c)
target_link_libraries(port_info ${PROJECT_NAME})

add_executable(port_config port_config.c)
target_link_libraries(port_config ${PROJECT_NAME})

add_executable(await_events await_events.c)
target_link_libraries(await_events ${PROJECT_NAME})

add_executable(handle_errors handle_errors.c)
target_link_libraries(handle_errors ${PROJECT_NAME})

add_executable(send_receive send_receive.c)
target_link_libraries(send_receive ${PROJECT_NAME})

