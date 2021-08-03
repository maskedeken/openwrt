#
# Copyright (C) 2018 Hao Dong <halbertdong@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-speederv2
PKG_VERSION:=1.1.0
PKG_RELEASE:=2

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Hao Dong <halbertdong@gmail.com>

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=luci
	CATEGORY:=LuCI
	SUBMENU:=3. Applications
	TITLE:=LuCI Support for speederv2-tunnel
	PKGARCH:=all
	DEPENDS:=+UDPspeeder
endef

define Package/$(PKG_NAME)/description
	LuCI Support for speederv2-tunnel.
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
	( . /etc/uci-defaults/luci-speederv2 ) && rm -f /etc/uci-defaults/luci-speederv2
fi
exit 0
endef

define Package/$(PKG_NAME)/conffiles
	/etc/config/speederv2
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/i18n
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/*.lmo $(1)/usr/lib/lua/luci/i18n/
	$(CP) ./root/* $(1)/
	$(CP) ./luasrc/* $(1)/usr/lib/lua/luci/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
