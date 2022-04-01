# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=subconverter
PKG_BASE_VERSION:=0.7.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/tindy2013/subconverter.git
PKG_SOURCE_DATE:=2022-03-20
PKG_SOURCE_VERSION:=406b0f20228b81d7ce06f2c4d49a5044fe015c23
PKG_MIRROR_HASH:=48b23fdc0d4059b139100df0ff0b9be4e339e8e513388e2e057ccfc34d2e59f7

PKG_VERSION:=$(PKG_BASE_VERSION)-$(PKG_SOURCE_DATE)-$(call version_abbrev,$(PKG_SOURCE_VERSION))

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Tianling Shen <cnsztl@immortalwrt.org>

PKG_BUILD_DEPENDS:=jpcre2 libcron quickjspp rapidjson toml11
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Utility to convert between various subscription format
  URL:=https://github.com/tindy2013/subconverter
  DEPENDS:=+libpthread +libstdcpp +libevent2 +libyaml-cpp +libpcre2 +libcurl +zlib
endef

define Package/$(PKG_NAME)/description
  Utility to convert between various proxy subscription formats.
endef

TARGET_CXXFLAGS := $(FPIC) $(filter-out -O%,$(TARGET_CXXFLAGS)) -O3
TARGET_CXXFLAGS += -Wall -Wextra -ffunction-sections -fdata-sections -flto
TARGET_LDFLAGS += -Wl,--gc-sections -flto

CMAKE_OPTIONS += -DCMAKE_BUILD_TYPE=Release

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/subconverter $(1)/usr/bin/subconverter
	$(INSTALL_DIR) $(1)/etc/subconverter
	$(CP) $(PKG_BUILD_DIR)/base/* $(1)/etc/subconverter/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/subconverter.init $(1)/etc/init.d/subconverter
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
