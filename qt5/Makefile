#
# Copyright (C) 2013 Riccardo Ferrazzo <f.riccardo87@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=qt5
PKG_VERSION:=5.0.2
PKG_RELEASE:=1
PKG_MD5SUM:=87cae8ae2f82f41ba027c2db0ab639b7

PKG_SOURCE:=qt-everywhere-opensource-src-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://download.qt-project.org/official_releases/qt/5.0/$(PKG_VERSION)/single
PKG_BUILD_DIR=$(BUILD_DIR)/qt-everywhere-opensource-src-$(PKG_VERSION)
PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=+python +python-bzip2
HOST_BUILD_DEPENDS:=+python/host +python-bzip2/host

include $(INCLUDE_DIR)/package.mk
$(call include_mk, python-package.mk)

define Package/qt5
  SECTION:=libraries
  CATEGORY:=Libraries
  TITLE:=qt5
  URL:=http://qt-project.org
  DEPENDS:=+zlib +libstdcpp @!LINUX_2_6
endef

define Build/Configure
	mkdir -p $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++
	$(CP) ./files/$(FILEPFX)qmake.conf $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qmake.conf
	$(CP) ./files/$(FILEPFX)qplatformdefs.h $(PKG_BUILD_DIR)/qtbase/mkspecs/linux-openwrt-g++/qplatformdefs.h
	( cd $(PKG_BUILD_DIR) ; \
		TARGET_CC="$(TARGET_CROSS)gcc" \
		TARGET_CXX="$(TARGET_CROSS)g++" \
		TARGET_AR="$(TARGET_CROSS)ar cqs" \
		TARGET_OBJCOPY="$(TARGET_CROSS)objcopy" \
		TARGET_RANLIB="$(TARGET_CROSS)ranlib" \
		TARGET_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
		TARGET_CXXFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
		TARGET_LDFLAGS="$(TARGET_LDFLAGS) $(EXTRA_LDFLAGS)" \
		TARGET_INCDIRS="$(TARGET_INCDIRS)" \
		TARGET_LIBDIRS="$(TARGET_LIBDIRS)" \
		PKG_CONFIG_SYSROOT="$(STAGING_DIR)" \
		CFLAGS= \
		CXXFLAGS= \
		LDFLAGS= \
		./configure \
			-arch mipsel \
			-no-c++11 \
			-sysroot $(STAGING_DIR) \
			-prefix $(CONFIGURE_PREFIX) \
			-bindir $(CONFIGURE_PREFIX)/bin \
			-libdir $(CONFIGURE_PREFIX)/lib \
			-datadir $(CONFIGURE_PREFIX)/share/Qt \
			-plugindir $(CONFIGURE_PREFIX)/lib/Qt/plugins \
			-xplatform linux-openwrt-g++ \
			-opensource \
			-confirm-license \
			-no-sql-db2 \
			-no-sql-ibase \
			-no-sql-mysql \
			-no-sql-oci \
			-no-sql-odbc \
			-no-sql-psql \
			-no-sql-sqlite \
			-no-sql-sqlite2 \
			-no-sql-tds \
			-no-qml-debug \
			-no-gif \
			-no-libpng \
			-no-libjpeg \
			-no-xcb \
			-no-strip \
			-openssl \
			-no-gui \
			-no-widgets \
			-no-nis \
			-no-cups \
			-no-dbus \
			-no-eglfs \
			-no-directfb \
			-no-linuxfb \
			-no-kms \
			-no-opengl \
			-no-javascript-jit \
			-make libs \
			-nomake webkit \
			-nomake docs \
			-nomake examples \
			-nomake demos \
			-nomake tests \
			-skip qtdeclarative \
			-skip qtjsbackend \
			-v \
	)
#TODO: add configure options
endef

define Build/Compile
	export PYTHONPATH="$(PYTHON_LIB_DIR):$(STAGING_DIR)/$(PYTHON_PKG_DIR)"; \
	export PATH="$(STAGING_DIR)/usr/bin:$(PATH)"; \
	TARGET_CC="$(TARGET_CROSS)gcc" \
	TARGET_CXX="$(TARGET_CROSS)g++" \
	TARGET_AR="$(TARGET_CROSS)ar cqs" \
	TARGET_OBJCOPY="$(TARGET_CROSS)objcopy" \
	TARGET_RANLIB="$(TARGET_CROSS)ranlib" \
	TARGET_CFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
	TARGET_CXXFLAGS="$(TARGET_CFLAGS) $(EXTRA_CFLAGS)" \
	TARGET_LDFLAGS="$(TARGET_LDFLAGS) $(EXTRA_LDFLAGS)" \
	TARGET_INCDIRS="$(TARGET_INCDIRS)" \
	TARGET_LIBDIRS="$(TARGET_LIBDIRS)" \
	STAGING_DIR="$(STAGING_DIR)" \
	STAGING_DIR_HOST="$(STAGING_DIR)/../host" \
	PKG_CONFIG_SYSROOT="$(STAGING_DIR)" \
	$(MAKE) -C $(PKG_BUILD_DIR)
	INSTALL_ROOT=$(PKG_INSTALL_DIR) \
	$(MAKE) -C $(PKG_BUILD_DIR) install
endef

define Package/qt5/install
  #TODO: copy files
endef

$(eval $(call BuildPackage,qt5))

