#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=sf_eswitch
PKG_RELEASE:=1

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

define KernelPackage/sf_eswitch
  SUBMENU:=Network Devices
  TITLE:=Siflower SFAX8 extern gigabit switch support
  FILES:=$(PKG_BUILD_DIR)/sf_eswitch.ko
  DEPENDS+=+kmod-sf_gmac
  AUTOLOAD:=$(call AutoLoad,55,sf_eswitch,1)
  KCONFIG:=
endef

define KernelPackage/sf_eswitch/config
	if PACKAGE_kmod-sf_eswitch
		config SFAX8_GENL
			bool "Generic netlink support"
			depends on PACKAGE_kmod-sf_netlink
			default "n"

		config ESWITCH_LIGHT
			bool "use light eswitch"
			default "n"
	endif
endef


EXTRA_KCONFIG:= \
	CONFIG_NET_VENDOR_SIFLOWER=y \
	CONFIG_SFAX8_ESWITCH_DRIVER=m \

ifdef CONFIG_TARGET_siflower_sf19a28_mpw1
NOSTDINC_FLAGS += -DCONFIG_SF19A28_MPW1
endif

ifdef CONFIG_TARGET_siflower_sf19a28_fullmask
NOSTDINC_FLAGS += -DCONFIG_SF19A28_FULLMASK
endif

ifdef CONFIG_SFAX8_GENL
EXTRA_KCONFIG += CONFIG_SFAX8_GENL=y
NOSTDINC_FLAGS += -DCONFIG_SFAX8_GENL
endif

ifdef CONFIG_ESWITCH_LIGHT
EXTRA_KCONFIG += CONFIG_ESWITCH_LIGHT=y
NOSTDINC_FLAGS += -DCONFIG_ESWITCH_LIGHT
endif

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./* $(PKG_BUILD_DIR)/
endef

define Build/Compile
endef

$(eval $(call KernelPackage,sf_eswitch))
