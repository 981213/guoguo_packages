# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2023 Luca Barbato

include $(TOPDIR)/rules.mk

PKG_NAME:=phantun
PKG_VERSION:=0.6.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/dndx/phantun/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=skip

PKG_MAINTAINER:=Chuanhong Guo <gch981213@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=rust/host
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/rust/rust-package.mk

define Package/phantun
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Fake UDP packets with TCP header
  DEPENDS:=$(RUST_ARCH_DEPENDS) +kmod-tun
  URL:=https://github.com/dndx/phantun
endef

define Package/phantun/description
  Fake UDP packets with TCP header
endef

define Build/Compile
	+$(CARGO_PKG_VARS) \
	cargo build \
		--profile $(CARGO_PKG_PROFILE) \
		$(if $(filter --jobserver%,$(PKG_JOBS)),,-j1) \
		--manifest-path "$(PKG_BUILD_DIR)/$(if $(strip $(1)),$(strip $(1)))/Cargo.toml"
endef

define Package/phantun/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/phantun.conf $(1)/etc/config/phantun
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/phantun.init $(1)/etc/init.d/phantun
	$(INSTALL_DIR) $(1)/usr/bin
	eval $(INSTALL_BIN) $(PKG_BUILD_DIR)/target/*-linux-*/release/client $(1)/usr/bin/phantun_client
endef

$(eval $(call BuildPackage,phantun))
