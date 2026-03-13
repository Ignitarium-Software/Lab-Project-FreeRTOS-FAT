add_library(freertos_plus_fat_port STATIC)

target_sources(freertos_plus_fat_port
    PRIVATE
    ff_sddisk.c
    ff_socfpga.c
    )

if(ENABLE_TINYUSB)
    target_sources(freertos_plus_fat_port PRIVATE
        ${FREERTOS_TOP_DIR}/tinyusb/apps/msc_app.c
    )
    target_link_libraries(freertos_plus_fat_port
        PRIVATE
        agilex5-tinyusb
    )
endif()

target_include_directories(freertos_plus_fat_port
    PUBLIC
    .
    ${FREERTOS_TOP_DIR}/drivers/sdmmc/
    )

target_link_libraries(freertos_plus_fat_port
  PUBLIC
    freertos_plus_fat_port_common
  PRIVATE
    freertos_kernel
    freertos_plus_fat
    socfpga_drivers
    )
