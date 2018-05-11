#
# Copyright (C) 2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=lorawan
PKG_RELEASE:=1

PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

include $(INCLUDE_DIR)/package.mk

define Package/lorawan
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=lorawan mac src
	DEPENDS:= +libpthread librt
endef

define Build/Prepare  
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./* $(PKG_BUILD_DIR)
endef 

#define Build/Configure

#endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR)/lib \
        CC="$(TARGET_CC)" \
        CFLAGS="$(TARGET_CFLAGS) -Wall" \
        LDFLAGS="$(TARGET_LDFLAGS)"
	$(MAKE) -C $(PKG_BUILD_DIR)/src \
        CC="$(TARGET_CC)" \
        CFLAGS="$(TARGET_CFLAGS) -Wall" \
        LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/lorawan/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/lorawan $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc/lorawan/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/global_conf.json $(1)/etc/lorawan/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/local_conf.json $(1)/etc/lorawan/
endef

$(eval $(call BuildPackage,lorawan))
