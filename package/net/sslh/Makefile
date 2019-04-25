#
# Copyright (C) 2009-2017 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# http://rutschle.net/tech/sslh/sslh-v1.20.tar.gz

# LOCAL_SRC $(TOPDIR)/build_dir/target-mipsel_mips32r2_uClibc-1.0.17/sslh-v1.2/
# BIN       $(TOPDIR)/bin/targets/mipselsf/generic-uClibc/packages/
# make package/sslh/clean # clear /bin /build_dir.

# Make patch
# cd ~/entware/sslh
# edit Makefile
# git diff > ~/entware/Entware-ng/sslh/patches/001-no_sslh_select.patch

# Compile ToDo
# cd ~/entware/Entware-ng/
# make package/sslh/compile -j1 V=s

include $(TOPDIR)/rules.mk

PKG_NAME:=sslh
PKG_VERSION:=v1.20
PKG_RELEASE:=2


PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://rutschle.net/tech/sslh/
PKG_HASH:=a7f49b0a1cfcb7bb9d97f5ffa932bff11c5f65d9a9bd8fe1812481dee5855116
PKG_LICENSE:=GPL-2.0+
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/sslh
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Routing and Redirection
  TITLE:=SSL/SSH multiplexer
  DEPENDS:=+libconfig +USE_UCLIBC:libpcre +USE_MUSL:libpcre
  URL:=http://rutschle.net/tech/sslh.shtml
  PKG_MAINTAINER:=Jonathan McCrohan <jmccrohan@gmail.com>
endef

define Package/sslh/conffiles
#/opt/etc/config/sslh
/opt/etc/sslh.cfg
endef

MAKE_FLAGS += \
  $(if $(CONFIG_USE_GLIBC),USELIBPCRE=,USELIBPCRE=1)

define Package/sslh/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sslh-fork $(1)/opt/sbin/sslh
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) files/S14$(PKG_NAME) $(1)/opt/etc/init.d
  #$(INSTALL_DIR) $(1)/opt/etc/config
  #$(INSTALL_CONF) files/$(PKG_NAME).config $(1)/opt/etc/config/$(PKG_NAME)
	$(INSTALL_CONF) files/sslh.cfg $(1)/opt/etc/sslh.cfg
endef

$(eval $(call BuildPackage,sslh))
