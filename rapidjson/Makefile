#
# Copyright (c) 2015 Affinegy, Inc. All rights reserved.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rapidjson
#PKG_VERSION:=1.0.2
#PKG_RELEASE:=1
#PKG_BUILD_DIR:=$(BUILD_DIR)/rapidjson-$(PKG_VERSION)
#PKG_SOURCE:=v$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=https://github.com/miloyip/rapidjson/archive
PKG_VERSION:=1.1.0-dev
PKG_RELEASE:=1
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Tencent/rapidjson.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=dfbe1db9da455552f7a9ad5d2aea17dd9d832ac1
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
CMAKE_INSTALL:=1
PKG_CAT:=zcat
PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=lib
  CATEGORY:=Libraries
  URL:=https://github.com/Tencent/rapidjson
  TITLE:=rapidjson JSON parser/generator for C++
  MAINTAINER:=Milo Yip <miloyip@gmail.com>
  DEPENDS:=
  MENU:=1
endef

define Package/$(PKG_NAME)/description
  A fast JSON parser/generator for C++ with both SAX/DOM style API
endef

define Build/Configure
  $(call Build/Configure/Default)
endef

define Build/Compile
endef

define Build/InstallDev
	mkdir -p $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/rapidjson $(1)/usr/include/rapidjson
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
