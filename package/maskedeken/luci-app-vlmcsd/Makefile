#
# Copyright (C) 2008-2014 The LuCI Team <luci@lists.subsignal.org>
#
# This is free software, licensed under the Apache License, Version 2.0 .
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-vlmcsd
PKG_VERSION:=1.0
PKG_RELEASE:=5

PKG_MAINTAINER:=cokebar <cokebar@cokebar.info>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
        SECTION:=luci
        CATEGORY:=LuCI
        SUBMENU:=3. Applications
        TITLE:=LuCI page for KMS
        PKGARCH:=all
        DEPENDS:=+vlmcsd
endef

define Package/$(PKG_NAME)/description
        LuCI Support for KMS.
endef

define Build/Prepare
        $(foreach po,$(wildcard ${CURDIR}/po/zh_Hans/*.po), \
                po2lmo $(po) $(PKG_BUILD_DIR)/$(patsubst %.po,%.lmo,$(notdir $(po)));)
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
        ( . /etc/uci-defaults/luci-app-vlmcsd ) && rm -f /etc/uci-defaults/luci-app-vlmcsd
fi
exit 0
endef

define Package/$(PKG_NAME)/conffiles
        /etc/config/vlmcsd
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/*.lmo $(1)/usr/lib/lua/luci/i18n/
	$(CP) ./root/* $(1)/
	$(CP) ./luasrc/* $(1)/usr/lib/lua/luci/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
