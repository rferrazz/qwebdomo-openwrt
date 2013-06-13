#
# Copyright (C) 2013 Riccardo Ferrazzo <f.riccardo87@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# 

include $(TOPDIR)/rules.mk

PKG_NAME:=qwebdomo
PKG_VERSION:=0.5
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://github.com/rferrazz/QWebdomo.git
PKG_SOURCE_VERSION:=a938cf1ee284f207f223d84d5c35341e983ea551
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_BUILD_DEPENDS:=+qmake

include $(INCLUDE_DIR)/package.mk

define 	Package/qwebdomo
  CATEGORY:=WHIA
  SECTION:=library
  TITLE:=qwebdomo
  DEPENDS:=+qt5-qtcore +qt5-qtnetwork +qxmpp
endef

define Build/Compile
  qmake PREFIX=/usr QW_DEVICE=1
  
  $(MAKE) -C $(PKG_BUILD_DIR)
  INSTALL_ROOT=$(PKG_INSTALL_DIR) \
  $(MAKE) -C $(PKG_BUILD_DIR) install
endef

define Package/qwebdomo/install
#TODO: set install section properly
endef

$(eval $(call BuildPackage,qwebdomo))