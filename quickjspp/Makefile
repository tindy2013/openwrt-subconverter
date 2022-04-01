# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=quickjspp
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/ftk/quickjspp.git
PKG_SOURCE_DATE:=2021-12-05
PKG_SOURCE_VERSION:=b23a60a96219eb3fdba281b8a73ac6fa22df1704
PKG_MIRROR_HASH:=9d152fd401f3eca406597cc40b63758bf32bb7c42a4f4e0385725426d6b43710

PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_BUILD_PARALLEL:=1
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)
  SECTION:=lib
  CATEGORY:=Libraries
  URL:=https://github.com/ftk/quickjspp
  TITLE:=QuickJS wrapper for C++
  DEPENDS:=+libatomic +libpthread
  PROVIDES:=quickjs
endef

define Package/$(PKG_NAME)/description
  QuickJSPP is QuickJS wrapper for C++. It allows you to easily embed
  Javascript engine into your program.
endef

define Build/Install
	$(INSTALL_DIR) $(PKG_INSTALL_DIR)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/quickjs/libquickjs.a $(PKG_INSTALL_DIR)/usr/lib/
	$(INSTALL_DIR) $(PKG_INSTALL_DIR)/usr/include/quickjs/
	$(CP) $(PKG_BUILD_DIR)/quickjspp.hpp $(PKG_INSTALL_DIR)/usr/include/
	$(CP) $(PKG_BUILD_DIR)/quickjs/quickjs*.h $(PKG_INSTALL_DIR)/usr/include/quickjs/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
