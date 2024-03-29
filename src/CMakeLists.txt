

CMAKE_MINIMUM_REQUIRED(VERSION 3.1)
CMAKE_POLICY(SET CMP0007 NEW)

SET(LIBRARY_NAME    driver-sharp-memlcd)

PROJECT(${LIBRARY_NAME} C)

SET(PROJECT_DESCRIPTION     "Sharp Memory LED Driverr")
SET(PROJECT_AUTHOR_NAME     "Chintalagiri Shashank")
SET(PROJECT_AUTHOR_EMAIL    "shashank.chintalagiri@gmail.com")
SET(PROJECT_LICENSE         "GPLv3")
SET(PROJECT_VERSION_MAJOR   1)
SET(PROJECT_VERSION_MINOR   0)
SET(PROJECT_VERSION_PATCH   0)
SET(PROJECT_VERSION_TWEAK   0)

IF(NOT ${CMAKE_CURRENT_SOURCE_DIR} STREQUAL ${CMAKE_SOURCE_DIR})
    FALLBACK_DEFAULT(SHARP_MEMLCD_APPLICATION_INCLUDE "#include \"app/application.h\"")
    FALLBACK_DEFAULT(SHARP_MEMLCD_INTEGRATED_BUILD     1)
ELSE()
    FALLBACK_DEFAULT(SHARP_MEMLCD_INTEGRATED_BUILD     0)
ENDIF()

FALLBACK_DEFAULT(SHARP_MEMLCD_PANEL         SHARP_MEMLCD_LS013B4DN04)
FALLBACK_DEFAULT(SHARP_MEMLCD_SPI_CLK_FREQ  1000000UL)     

FALLBACK_DEFAULT(SHARP_MEMLCD_COMINV        SHARP_MEMLCD_COMINV_SW)

FALLBACK_DEFAULT(SHARP_MEMLCD_IMAGE_WRITER  1)
FALLBACK_DEFAULT(SHARP_MEMLCD_MANAGER       1)
FALLBACK_DEFAULT(SHARP_MEMLCD_FRAMEBUFFER   0)

INCLUDE(ebs/driver-conf)

ADD_FILES(HEADERS interface.h
                  memlcd.h
                  panels.h
                  vcom.h)

ADD_FILES(SOURCES memlcd.c 
                  vcom.c)

ADD_PLATFORM_LIBRARY(driver-sharp-memlcd STATIC "hal-uc-spi" ${SOURCES})

IF(${CMAKE_CURRENT_SOURCE_DIR} STREQUAL ${CMAKE_SOURCE_DIR})
    INSTALL_PLATFORM_LIBRARY(driver-sharp-memlcd ${HEADERS})
    INCLUDE(ebs/lib-doc)
ENDIF()
