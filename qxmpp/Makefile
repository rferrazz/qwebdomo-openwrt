#
# Copyright (C) 2013 Riccardo Ferrazzo <f.riccardo87@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=qxmpp
PKG_VERSION:=0.7.6
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://qxmpp.googlecode.com/files
PKG_MD5SUM:=ee45a97313306ded2ff0f6618a3ed1e1
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
$(call  include_mk, cmake.mk)

define 	Package/qxmpp
  CATEGORY:=Libraries
  SECTION:=libraries
  TITLE:=qxmpp
  DEPENDS:=+qt5-core +qt5-network +qt5-xml
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
	$(INSTALL_DIR) $(1)/usr/include/qxmpp
	$(INSTALL_DIR) $(1)/usr/lib
	
	$(CP) \
		$(PKG_BUILD_DIR)/src/base/*.h \
		$(1)/usr/include/qxmpp/

	$(CP) \
		$(PKG_BUILD_DIR)/src/client/*.h \
		$(1)/usr/include/qxmpp/

	$(CP) \
		$(PKG_BUILD_DIR)/src/server/*.h \
		$(1)/usr/include/qxmpp/
		
	$(CP) \
		$(PKG_BUILD_DIR)/libqxmpp.so* \
		$(1)/usr/lib/
endef

define Package/qxmpp/install
	$(INSTALL_DIR) $(1)/usr/lib

	$(CP) \
		$(PKG_BUILD_DIR)/libqxmpp.so* \
		$(1)/usr/lib/
endef

$(eval $(call BuildPackage,qxmpp))
