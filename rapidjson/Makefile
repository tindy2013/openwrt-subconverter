# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=rapidjson
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Tencent/rapidjson.git
PKG_SOURCE_DATE:=2021-11-24
PKG_SOURCE_VERSION:=fd3dc29a5c2852df569e1ea81dbde2c412ac5051
PKG_MIRROR_HASH:=4c9dbcfb7746202f7c9b7b4df78bd5349e7df21ee0f1fe816195eb013b4e194f

PKG_LICENSE:=BSD 3-Clause
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_BUILD_PARALLEL:=1
CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

CMAKE_OPTIONS+= -DRAPIDJSON_BUILD_DOC=OFF \
	-DRAPIDJSON_BUILD_EXAMPLES=OFF \
	-DRAPIDJSON_BUILD_TESTS=OFF

define Package/$(PKG_NAME)
  SECTION:=lib
  CATEGORY:=Libraries
  URL:=https://github.com/Tencent/rapidjson
  TITLE:=rapidjson JSON parser/generator for C++
endef

define Package/$(PKG_NAME)/description
  A fast JSON parser/generator for C++ with both SAX/DOM style API
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
