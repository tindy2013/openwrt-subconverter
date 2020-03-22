#
# Copyright (C) 2019-2020 XTindy
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=subconverter
PKG_VERSION:=0.4.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/tindy2013/subconverter.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=3560b3af934e1dffd7bdac2e5438456fa6632b4f
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
CMAKE_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_CONFIG_DEPENDS:= \
  CONFIG_SUBCONVERTER_OPENSSL \
  CONFIG_SUBCONVERTER_MBEDTLS \
  CONFIG_SUBCONVERTER_STDREGEX \
  CONFIG_SUBCONVERTER_PCRE2

PKG_BUILD_DEPENDS:=libevent2 libyaml-cpp curl rapidjson SUBCONVERTER_OPENSSL:openssl SUBCONVERTER_MBEDTLS:mbedtls SUBCONVERTER_PCRE2:pcre2

PKG_LICENSE:=GPL-3.0

PKG_MAINTAINER:=XTindy

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TARGET_CXXFLAGS += -Wall -Wextra
TARGET_CXXFLAGS += $(FPIC)

# LTO
TARGET_CXXFLAGS += -flto
TARGET_LDFLAGS += -flto

# CXX standard
TARGET_CXXFLAGS += -std=c++17

TARGET_CXXFLAGS := $(filter-out -O%,$(TARGET_CXXFLAGS)) -O3

TARGET_CXXFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

CMAKE_OPTIONS += \
	$(if $(CONFIG_SUBCONVERTER_STDREGEX),-DUSING_STD_REGEX=ON,) \
	$(if $(CONFIG_SUBCONVERTER_MBEDTLS),-DUSING_MBEDTLS=ON,) \
#	-DUSING_MALLOC_TRIM=ON

define Package/subconverter
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Utility to convert between various subscription format.
	URL:=https://github.com/tindy2013/subconverter
	DEPENDS:=+libpthread +libstdcpp \
		+libevent2 +libyaml-cpp +libcurl +SUBCONVERTER_PCRE2:libpcre2 +SUBCONVERTER_OPENSSL:libopenssl +SUBCONVERTER_MBEDTLS:libmbedtls
endef

define Package/subconverter/config
  source "$(SOURCE)/Config.in"
endef

define Package/subconverter/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/subconverter.init $(1)/etc/init.d/subconverter
	$(INSTALL_DIR) $(1)/usr/sbin/subconverter
	$(INSTALL_BIN) $(BUILD_DIR)/${PKG_SOURCE_SUBDIR}/subconverter $(1)/usr/sbin/subconverter
	$(CP) $(BUILD_DIR)/${PKG_SOURCE_SUBDIR}/base/* $(1)/usr/sbin/subconverter
endef


$(eval $(call BuildPackage,subconverter))
