include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/version.mk

PKG_NAME:=ath10k-boarddata-k2t
PKG_RELEASE:=1
PKG_FLAGS:=nonshared

include $(INCLUDE_DIR)/package.mk

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
endef

define Package/ath10k-boarddata-k2t
  SUBMENU:=ath10k Board-Specific Overrides
  TITLE:=board-2.bin Overrides for Phicomm K2T
  SECTION:=firmware
  CATEGORY:=Firmware
  DEPENDS:=@TARGET_ath79
endef

define Package/ath10k-boarddata-k2t/description
Phicomm K2T requires board-specific, reference ("cal") data and
a script to detect device variants and select corresponding board
data.

This package supplies board-2.bin file(s) that, in the interim,
overwrite those supplied by the ath10k-firmware-* packages.

This is package is only necessary for the Phicomm K2T.

Do not install it for any other device!
endef

define Package/ath10k-boarddata-k2t/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath10k/QCA9888/hw2.0/k2t
	$(INSTALL_DIR) $(1)/lib/preinit
	$(INSTALL_DATA) ./files/ath10k-boarddata* $(1)/lib/firmware/ath10k/QCA9888/hw2.0/k2t
	$(INSTALL_DATA) ./files/85-k2t-prepare-boarddata $(1)/lib/preinit
endef

$(eval $(call BuildPackage,ath10k-boarddata-k2t))
