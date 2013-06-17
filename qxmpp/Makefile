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

include $(INCLUDE_DIR)/package.mk
$(call	include_mk, qmake.mk)

define 	Package/qxmpp
  CATEGORY:=Libraries
  SECTION:=libraries
  TITLE:=qxmpp
  DEPENDS:=+qt5-core +qt5-network
endef

define Build/Configure
  $(call Build/Configure/Qmake,qxmpp)
endef

$(eval $(call BuildPackage,qxmpp))
