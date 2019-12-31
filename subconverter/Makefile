#
# Copyright (C) 2019-2020 XTindy
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=subconverter
PKG_VERSION:=0.2.2
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/tindy2013/subconverter.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=f7a7a4a15e93829bb4fc1d329ecd1a3ab63c5acc
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
CMAKE_INSTALL:=1
PKG_BUILD_PARALLEL:=1

PKG_BUILD_DEPENDS:=+libevent2 +libyaml-cpp +libcurl +openssl1.1

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
MY_OPENSSL_DIR:=$(BUILD_DIR)/openssl1.1_staging_dir/usr

TARGET_CXXFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

CMAKE_FIND_ROOT_PATH := $(MY_OPENSSL_DIR);$(CMAKE_FIND_ROOT_PATH)
TARGET_CXXFLAGS := -I$(MY_OPENSSL_DIR)/include $(TARGET_CXXFLAGS)
TARGET_LDFLAGS := -L$(MY_OPENSSL_DIR)/lib $(TARGET_LDFLAGS)

CMAKE_OPTIONS += \
	-DUSING_STD_REGEX=ON \
	-DUSING_MALLOC_TRIM=ON

define Package/subconverter
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Utility to convert between various subscription format.
	URL:=https://github.com/tindy2013/subconverter
	DEPENDS:=+libpthread +libstdcpp \
		+libevent2 +libyaml-cpp +libcurl +libopenssl
endef



define Package/subconverter/install
	$(INSTALL_DIR) $(1)/usr/sbin/subconverter
	$(INSTALL_BIN) $(BUILD_DIR)/${PKG_SOURCE_SUBDIR}/subconverter $(1)/usr/sbin/subconverter
	$(CP) $(BUILD_DIR)/${PKG_SOURCE_SUBDIR}/base/* $(1)/usr/sbin/subconverter
endef


$(eval $(call BuildPackage,subconverter))
