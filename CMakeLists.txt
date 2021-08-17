cmake_minimum_required(VERSION 3.7)

project(halflife)

#set(CMAKE_CXX_STANDARD 20)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)

#list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

add_definitions(-w -g -D_DEBUG)

set(SOURCE_DIR ${CMAKE_SOURCE_DIR})

set(HL_SRC_DIR ${SOURCE_DIR}/cl_dll)
set(HL_SERVER_SRC_DIR ${SOURCE_DIR}/dlls)
set(GAME_SHARED_SRC_DIR ${SOURCE_DIR}/game_shared)
set(PM_SHARED_SRC_DIR ${SOURCE_DIR}/pm_shared)

set(PUBLIC_SRC_DIR ${SOURCE_DIR}/public)
set(COMMON_SRC_DIR ${SOURCE_DIR}/common)

if(UNIX)
    add_definitions(-DNDEBUG -DPOSIX -D_POSIX -DGNUC -DHL1 -Dstricmp=strcasecmp -D_strnicmp=strncasecmp -Dstrnicmp=strncasecmp -D_snprintf=snprintf -DQUIVER -DQUAKE2 -DVALVE_DLL -D_alloca=alloca -D_vsnprintf=vsnprintf -DNO_MALLOC_OVERRIDE)
    if(APPLE)
        add_definitions(-DOSX -D_OSX)
    else()
        add_definitions(-DLINUX -D_LINUX)
    endif()
endif()
# DEDICATED_CFLAGS="-DDEDICATED -DSWDS"

add_definitions(-DCLIENT_DLL -DCLIENT_WEAPONS -DHL_DLL -D_snwprintf=swprintf -DDISABLE_JUMP_ORIGIN -DDISABLE_VEC_ORIGIN)

include_directories(
${HL_SRC_DIR}
${HL_SERVER_SRC_DIR}
${SOURCE_DIR}/tfc
${COMMON_SRC_DIR}
${PUBLIC_SRC_DIR}
${PM_SHARED_SRC_DIR}
${SOURCE_DIR}/engine
${SOURCE_DIR}/utils/vgui/include
${GAME_SHARED_SRC_DIR}
${SOURCE_DIR}/external)


set(HL1_SRCS
${HL_SRC_DIR}/hud_spectator.cpp
${HL_SRC_DIR}/ev_hldm.cpp
${HL_SRC_DIR}/hl/hl_baseentity.cpp
${HL_SRC_DIR}/hl/hl_events.cpp
${HL_SRC_DIR}/hl/hl_objects.cpp
${HL_SRC_DIR}/hl/hl_weapons.cpp
${HL_SRC_DIR}/hud.cpp
${HL_SRC_DIR}/inputw32.cpp
${HL_SRC_DIR}/ammo.cpp
${HL_SRC_DIR}/ammo_secondary.cpp
${HL_SRC_DIR}/ammohistory.cpp
${HL_SRC_DIR}/battery.cpp
${HL_SRC_DIR}/cdll_int.cpp
${HL_SRC_DIR}/com_weapons.cpp
${HL_SRC_DIR}/death.cpp
${HL_SRC_DIR}/demo.cpp
${HL_SRC_DIR}/entity.cpp
${HL_SRC_DIR}/ev_common.cpp
${HL_SRC_DIR}/events.cpp
${HL_SRC_DIR}/flashlight.cpp
${HL_SRC_DIR}/GameStudioModelRenderer.cpp
${HL_SRC_DIR}/geiger.cpp
${HL_SRC_DIR}/health.cpp
${HL_SRC_DIR}/hud_bench.cpp
${HL_SRC_DIR}/hud_benchtrace.cpp
${HL_SRC_DIR}/hud_msg.cpp
${HL_SRC_DIR}/hud_redraw.cpp
${HL_SRC_DIR}/hud_update.cpp
${HL_SRC_DIR}/in_camera.cpp
${HL_SRC_DIR}/input.cpp
${HL_SRC_DIR}/interpolation.cpp
${HL_SRC_DIR}/menu.cpp
${HL_SRC_DIR}/message.cpp
${HL_SRC_DIR}/saytext.cpp
${HL_SRC_DIR}/status_icons.cpp
${HL_SRC_DIR}/statusbar.cpp
${HL_SRC_DIR}/studio_util.cpp
${HL_SRC_DIR}/StudioModelRenderer.cpp
${HL_SRC_DIR}/text_message.cpp
${HL_SRC_DIR}/train.cpp
${HL_SRC_DIR}/tri.cpp
${HL_SRC_DIR}/util.cpp
${HL_SRC_DIR}/view.cpp
${HL_SRC_DIR}/vgui_int.cpp
${HL_SRC_DIR}/vgui_ClassMenu.cpp
${HL_SRC_DIR}/vgui_ConsolePanel.cpp
${HL_SRC_DIR}/vgui_ControlConfigPanel.cpp
${HL_SRC_DIR}/vgui_CustomObjects.cpp
${HL_SRC_DIR}/vgui_MOTDWindow.cpp
${HL_SRC_DIR}/vgui_SchemeManager.cpp
${HL_SRC_DIR}/vgui_ScorePanel.cpp
${HL_SRC_DIR}/vgui_ServerBrowser.cpp
${HL_SRC_DIR}/vgui_TeamFortressViewport.cpp
${HL_SRC_DIR}/vgui_SpectatorPanel.cpp
${HL_SRC_DIR}/vgui_teammenu.cpp
${HL_SRC_DIR}/voice_status.cpp
${HL_SRC_DIR}/hud_servers.cpp)
	

set(DLL_SRCS
${HL_SERVER_SRC_DIR}/crossbow.cpp
${HL_SERVER_SRC_DIR}/crowbar.cpp
${HL_SERVER_SRC_DIR}/egon.cpp
${HL_SERVER_SRC_DIR}/gauss.cpp
${HL_SERVER_SRC_DIR}/handgrenade.cpp
${HL_SERVER_SRC_DIR}/hornetgun.cpp
${HL_SERVER_SRC_DIR}/mp5.cpp
${HL_SERVER_SRC_DIR}/python.cpp
${HL_SERVER_SRC_DIR}/rpg.cpp
${HL_SERVER_SRC_DIR}/satchel.cpp
${HL_SERVER_SRC_DIR}/shotgun.cpp
${HL_SERVER_SRC_DIR}/squeakgrenade.cpp
${HL_SERVER_SRC_DIR}/tripmine.cpp
${HL_SERVER_SRC_DIR}/wpn_shared/hl_wpn_glock.cpp)


set(PUBLIC_SRCS ${PUBLIC_SRC_DIR}/interface.cpp)

set(COMMON_SRCS	${COMMON_SRC_DIR}/parsemsg.cpp)

set(GAME_SHARED_SRCS
${GAME_SHARED_SRC_DIR}/vgui_checkbutton2.cpp
${GAME_SHARED_SRC_DIR}/vgui_grid.cpp
${GAME_SHARED_SRC_DIR}/vgui_helpers.cpp
${GAME_SHARED_SRC_DIR}/vgui_listbox.cpp
${GAME_SHARED_SRC_DIR}/vgui_loadtga.cpp
${GAME_SHARED_SRC_DIR}/vgui_scrollbar2.cpp
${GAME_SHARED_SRC_DIR}/vgui_slider2.cpp
${GAME_SHARED_SRC_DIR}/voice_banmgr.cpp)
	
set(PM_SHARED_SRCS
${PM_SHARED_SRC_DIR}/pm_debug.c
${PM_SHARED_SRC_DIR}/pm_shared.c
${PM_SHARED_SRC_DIR}/pm_math.c)

add_executable(client ${HL1_SRCS} ${PUBLIC_SRCS} ${COMMON_SRCS} ${GAME_SHARED_SRCS} ${DLL_SRCS} ${PM_SHARED_SRCS})


