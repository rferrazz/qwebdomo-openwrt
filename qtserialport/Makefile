#
# Copyright (C) 2013 Riccardo Ferrazzo <f.riccardo87@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=qtserialport
PKG_VERSION:=5.1.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://gitorious.org/qt/qtserialport.git
PKG_SOURCE_VERSION:=39f90528abda2f5ec7575acf2e1a352702a202e8
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_BUILD_DEPENDS:=+qt5-core

include $(INCLUDE_DIR)/package.mk
$(call	include_mk, cmake.mk)

define 	Package/qtserialport
  CATEGORY:=Libraries
  SECTION:=libraries
  TITLE:=qtserialport
  DEPENDS:=+qt5-core
endef

ifeq ($(CONFIG_CCACHE),)
  CMAKE_C_COMPILER:=$(TOOLCHAIN_DIR)/bin/$(TARGET_CC)
  CMAKE_C_COMPILER_ARG1:=
  CMAKE_CXX_COMPILER:=$(TOOLCHAIN_DIR)/bin/$(TARGET_CXX)
  CMAKE_CXX_COMPILER_ARG1:=
else
  CMAKE_C_COMPILER:=$(STAGING_DIR_HOST)/bin/ccache
  CMAKE_C_COMPILER_ARG1:=$(filter-out ccache,$(TARGET_CC))
  CMAKE_CXX_COMPILER:=$(STAGING_DIR_HOST)/bin/ccache
  CMAKE_CXX_COMPILER_ARG1:=$(filter-out ccache,$(TARGET_CXX))
endif

define Build/Configure
	$(CP) ./files/CMakeLists.txt $(PKG_BUILD_DIR)
	$(INSTALL_DIR) $(PKG_INSTALL_DIR)/usr/include/QtSerialPort
	$(CP) ./files/Q* $(PKG_INSTALL_DIR)/usr/include/QtSerialPort/
	$(CP) $(PKG_BUILD_DIR)/src/serialport/*.h $(PKG_INSTALL_DIR)/usr/include/QtSerialPort/
	( cd $(PKG_BUILD_DIR); \
	CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
	CXXFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
	LD_LIBRARY_PATH="$(TARGET_LIBDIRS) $(STAGING_DIR)/usr/lib/" \
	cmake \
		-DCMAKE_SYSTEM_NAME=Linux \
		-DCMAKE_SYSTEM_VERSION=1 \
		-DCMAKE_SYSTEM_PROCESSOR=$(ARCH) \
		-DCMAKE_BUILD_TYPE=Debug \
		-DCMAKE_C_FLAGS_RELEASE="-DNDEBUG" \
		-DCMAKE_CXX_FLAGS_RELEASE="-DNDEBUG" \
		-DCMAKE_RUNTIME_OUTPUT_DIRECTORY="$(PKG_INSTALL_DIR)" \
		-DCMAKE_C_COMPILER="$(CMAKE_C_COMPILER)" \
		-DCMAKE_C_COMPILER_ARG1="$(CMAKE_C_COMPILER_ARG1)" \
		-DCMAKE_CXX_COMPILER="$(CMAKE_CXX_COMPILER)" \
		-DCMAKE_CXX_COMPILER_ARG1="$(CMAKE_CXX_COMPILER_ARG1)" \
		-DCMAKE_EXE_LINKER_FLAGS="$(TARGET_LDFLAGS)" \
		-DCMAKE_MODULE_LINKER_FLAGS="$(TARGET_LDFLAGS)" \
		-DCMAKE_SHARED_LINKER_FLAGS="$(TARGET_LDFLAGS)" \
		-DCMAKE_FIND_ROOT_PATH=$(STAGING_DIR) \
		-DCMAKE_FIND_ROOT_PATH_MODE_PROGRAM=BOTH \
		-DCMAKE_FIND_ROOT_PATH_MODE_LIBRARY=ONLY \
		-DCMAKE_FIND_ROOT_PATH_MODE_INCLUDE=ONLY \
		-DCMAKE_STRIP=: \
		-DCMAKE_INSTALL_PREFIX=/usr \
		$(CMAKE_OPTIONS) \
		. \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/QtSerialPort
	$(INSTALL_DIR) $(1)/usr/lib

	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/QtSerialPort/* \
		$(1)/usr/include/QtSerialPort/

	$(CP) \
		$(PKG_BUILD_DIR)/libqtserialport.so* \
		$(1)/usr/lib/
endef

define Package/qtserialport/install
	$(INSTALL_DIR) $(1)/usr/lib
	
	$(CP) \
		$(PKG_BUILD_DIR)/libqtserialport.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,qtserialport))
