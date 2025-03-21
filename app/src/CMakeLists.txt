add_subdirectory(classification)

set(APP_DISPATCHER_SOURCE_DIR ${APP_SUPPORT_PACKAGE}/app_dispatcher)
set(LCM_SOURCE_DIR ${APP_SUPPORT_PACKAGE}/life_cycle_manager)
set(APP_BIN ${CMAKE_HOME_DIRECTORY}/bin)
set(APP_LIBS ${CMAKE_HOME_DIRECTORY}/libs)
set(APP_RES ${CMAKE_HOME_DIRECTORY}/res)
set(APP_STORAGE ${CMAKE_HOME_DIRECTORY}/storage)

# Get app_dispatcher binary and manifests from AppSupportPackage
file(MAKE_DIRECTORY ${APP_LIBS})
file(COPY ${APP_DISPATCHER_SOURCE_DIR} DESTINATION ${APP_LIBS})

# Create res, res/models
file(MAKE_DIRECTORY ${APP_RES})
file(MAKE_DIRECTORY ${APP_RES}/models)
file(MAKE_DIRECTORY ${APP_RES}/settings)

# Create storage, storage/settings
file(MAKE_DIRECTORY ${APP_STORAGE})
file(MAKE_DIRECTORY ${APP_STORAGE}/settings)

# Get application execution binary and LCM manifests from AppSupportPackage
# - this operation is executed in cmake command running time, not build time
file(MAKE_DIRECTORY ${APP_BIN})
file(COPY ${LCM_SOURCE_DIR}/ DESTINATION ${APP_BIN}/)
file(RENAME ${APP_BIN}/life_cycle_manager ${APP_BIN}/${PROJECT_NAME})

# Copy google_net model
set(SDK_AI_BIN ${COMMON}/ai_bin/${SOC})
file(COPY ${SDK_AI_BIN}/ DESTINATION ${APP_RES}/ai_bin/)

# install PLifeCycleManagermanifest.json
install (FILES ${CMAKE_CURRENT_SOURCE_DIR}/PLifeCycleManagermanifest.json DESTINATION ${APP_BIN})