#
# Copyright (C) 2012-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=odhcp6c
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/sbyx/odhcp6c.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2016-12-16
PKG_SOURCE_VERSION:=7533a6243dc3ac5a747cf6ccbc4d0539dafd3e07
PKG_MIRROR_HASH:=c5e586bc9b913a79f311cbb4fd1c6ba589220948dd0e0156903c1e7870bbdbeb
PKG_MAINTAINER:=Steven Barth <steven@midlink.org>
PKG_LICENSE:=GPL-2.0

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

ifneq ($(CONFIG_PACKAGE_odhcp6c_ext_cer_id),0)
  CMAKE_OPTIONS += -DEXT_CER_ID=$(CONFIG_PACKAGE_odhcp6c_ext_cer_id)
endif

define Package/odhcp6c
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Embedded DHCPv6-client for OpenWrt
  DEPENDS:=@IPV6
endef

define Package/odhcp6c/config
  config PACKAGE_odhcp6c_ext_cer_id
    int "CER-ID Extension ID (0 = disabled)"
    depends on PACKAGE_odhcp6c
    default 0
endef

define Package/odhcp6c/install
	$(INSTALL_DIR) $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/odhcp6c $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/lib/netifd/proto
	$(INSTALL_BIN) ./files/dhcpv6.sh $(1)/lib/netifd/proto/dhcpv6.sh
	$(INSTALL_BIN) ./files/dhcpv6.script $(1)/lib/netifd/
endef

$(eval $(call BuildPackage,odhcp6c))
