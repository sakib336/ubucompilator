add_custom_target (i18n ALL COMMENT “Building i18n messages.”)
file (GLOB LIBPANTHEON_PO_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.po)
foreach (LIBPANTHEON_PO_INPUT ${LIBPANTHEON_PO_FILES})
    get_filename_component (LIBPANTHEON_PO_INPUT_BASE ${LIBPANTHEON_PO_INPUT} NAME_WE)
    set (LIBPANTHEON_MO_OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/${LIBPANTHEON_PO_INPUT_BASE}.mo)
    add_custom_command (TARGET i18n COMMAND msgfmt -o ${LIBPANTHEON_MO_OUTPUT} ${LIBPANTHEON_PO_INPUT})

    install (FILES ${LIBPANTHEON_MO_OUTPUT} DESTINATION share/locale-langpack/${LIBPANTHEON_PO_INPUT_BASE}/LC_MESSAGES RENAME libpantheon.mo)
endforeach (LIBPANTHEON_PO_INPUT ${LIBPANTHEON_PO_FILES})

add_custom_target (catalog COMMENT “Building catalog.”)
set(LIBPANTHEON_C_FILES 
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/ModeButton.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/DatePicker.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/Entries.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/TimePicker.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/CollapsiblePaned.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/AppMenu.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/Welcome.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Widgets/ToolButtonWithMenu.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Services/Settings.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Services/Logger.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Services/Paths.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Services/System.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/AppFactory.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Application.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Drawing/Color.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Drawing/BufferSurface.vala
    ${CMAKE_CURRENT_SOURCE_DIR}/../lib/Drawing/Utilities.vala)
add_custom_command(TARGET catalog  COMMAND xgettext -d ${GETTEXT_PACKAGE} -s -o ${CMAKE_CURRENT_SOURCE_DIR}/libpantheon.pot ${LIBPANTHEON_C_FILES} --from-code UTF-8 -L C\# -k_)
