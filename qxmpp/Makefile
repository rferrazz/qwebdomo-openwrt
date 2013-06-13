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

PKG_SOURCE_URL:=https://qxmpp.googlecode.com/files
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_BUILD_DEPENDS:=+qmake

include $(INCLUDE_DIR)/package.mk

define 	Package/qxmpp
  CATEGORY:=libraries
  SECTION:=library
  TITLE:=qxmpp
  DEPENDS:=+qt5-qtcore +qt5-qtnetwork
endef

define Build/Compile
  qmake PREFIX=/usr
  
  $(MAKE) -C $(PKG_BUILD_DIR)
  INSTALL_ROOT=$(PKG_INSTALL_DIR) \
  $(MAKE) -C $(PKG_BUILD_DIR) install
endef

define Package/qxmpp/install
#TODO: add install step
endef

$(eval $(call BuildPackage,qxmpp))