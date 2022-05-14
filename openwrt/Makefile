include $(TOPDIR)/rules.mk

PKG_NAME:=r8168
PKG_VERSION:=8.05.0
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=r8168-8.05.0.tar
PKG_SOURCE_URL:=https://go.koalabear.tk/
PKG_HASH:=93f5a866155d0e07d46d19cf8a6e17643b22e629e31677889714cefd8dd785ec

PKG_MAINTAINER:=koala <koalabearguo@gmail.com>
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

TAR_OPTIONS+= --strip-components 1
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

define KernelPackage/r8168
        SUBMENU:=Network Devices
        TITLE:=RealTek RTL-8168 PCI Gigabit Ethernet Adapter kernel support
	URL:=https://github.com/koalabearguo/rtl8186-driver
        DEPENDS:=@PCI_SUPPORT +kmod-mii +r8169-firmware +kmod-phy-realtek
	FILES:=$(PKG_BUILD_DIR)/src/r8168.ko
        AUTOLOAD:=$(call AutoProbe,r8168)
endef

# The last two DEPENDS are hacks in order to get CONFIG_ASN1 and CONFIG_OID_REGISTRY
# which it seems can't be selected independently. Some bug in either base or upstream.

define KernelPackage/r8168/description
 Kernel modules for RealTek RTL-8168 PCI Gigabit Ethernet adapters
endef

define Build/Compile
	$(KERNEL_MAKE) M="$(PKG_BUILD_DIR)/src" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" $(PKG_EXTRA_KCONFIG) \
	modules
endef

$(eval $(call KernelPackage,r8168))
