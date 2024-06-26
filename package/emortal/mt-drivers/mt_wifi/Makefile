#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mt_wifi
PKG_VERSION:=2
PKG_RELEASE:=2

PKG_CONFIG_DEPENDS := \
	CONFIG_MTK_CHIP_MT7603E_MT7612E \
	CONFIG_MTK_CHIP_MT7603E_MT7615E \
	CONFIG_MTK_CHIP_MT7615E \
	CONFIG_MTK_CHIP_MT7615E_DBDC \
	CONFIG_MTK_CHIP_MT7915E_DBDC

include $(INCLUDE_DIR)/package.mk

define Package/mt_wifi
  SECTION:=net
  CATEGORY:=Network
  TITLE:=MTK wifi AP config
  DEPENDS:=@TARGET_ramips +wireless-tools
  SUBMENU:=Wireless
endef

define Package/mt_wifi/config
	source "$(SOURCE)/config.in"
endef

define Package/mt_wifi/description
  MT_WiFi auto config for mt7603/mt7612/mt7615 chips
endef

define Build/Compile
endef

define Package/mt_wifi/install
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/lib/wifi/
	$(INSTALL_DIR) $(1)/etc/wireless/mt7615/
	$(INSTALL_DIR) $(1)/etc_ro/Wireless/RT2860AP/
	$(INSTALL_DIR) $(1)/lib/preinit/
ifeq ($(CONFIG_MTK_CHIP_MT7603E_MT7612E),y)
	$(INSTALL_BIN) ./files/7603_7612-l1profile.dat $(1)/etc/wireless/l1profile.dat
	$(INSTALL_BIN) ./files/mt7603.dat $(1)/etc/wireless/mt7615/mt7615.1.dat
	$(INSTALL_BIN) ./files/mt7612.dat $(1)/etc/wireless/mt7615/mt7615.2.dat
	$(INSTALL_BIN) ./files/apcli_7612.sh $(1)/etc/init.d/apcli.sh
else ifeq ($(CONFIG_MTK_CHIP_MT7603E_MT7615E),y)
	$(INSTALL_BIN) ./files/7603_7615-l1profile.dat $(1)/etc/wireless/l1profile.dat
	$(INSTALL_BIN) ./files/mt7603.dat $(1)/etc/wireless/mt7615/mt7615.1.dat
	$(INSTALL_BIN) ./files/mt7615.5G.dat $(1)/etc/wireless/mt7615/mt7615.2.dat
	$(INSTALL_BIN) ./files/apcli_7615.sh $(1)/etc/init.d/apcli.sh
else ifeq ($(CONFIG_MTK_CHIP_MT7615E_DBDC),y)
	$(INSTALL_BIN) ./files/7615d.l1profile.dat $(1)/etc/wireless/l1profile.dat
	$(INSTALL_BIN) ./files/mt7615.1.2G.dat $(1)/etc/wireless/mt7615/
	$(INSTALL_BIN) ./files/mt7615.1.5G.dat $(1)/etc/wireless/mt7615/
	$(INSTALL_BIN) ./files/apcli_7615d.sh $(1)/etc/init.d/apcli.sh
else ifeq ($(CONFIG_MTK_CHIP_MT7915E_DBDC),y)
	$(INSTALL_BIN) ./files/7915d.l1profile.dat $(1)/etc/wireless/l1profile.dat
	$(INSTALL_BIN) ./files/mt7915.1.2G.dat $(1)/etc/wireless/mt7615/
	$(INSTALL_BIN) ./files/mt7915.1.5G.dat $(1)/etc/wireless/mt7615/
	$(INSTALL_BIN) ./files/apcli_7615d.sh $(1)/etc/init.d/apcli.sh
else
	$(INSTALL_BIN) ./files/7615.l1profile.dat $(1)/etc/wireless/l1profile.dat
	$(INSTALL_BIN) ./files/mt7615.2G.dat $(1)/etc/wireless/mt7615/mt7615.1.dat
	$(INSTALL_BIN) ./files/mt7615.5G.dat $(1)/etc/wireless/mt7615/mt7615.2.dat
	$(INSTALL_BIN) ./files/apcli_7615.sh $(1)/etc/init.d/apcli.sh
endif
	$(INSTALL_BIN) ./files/SingleSKU.dat $(1)/etc_ro/Wireless/RT2860AP/
	$(INSTALL_BIN) ./files/SingleSKU_BF.dat $(1)/etc_ro/Wireless/RT2860AP/
	$(INSTALL_BIN) ./files/mt7615.lua $(1)/lib/wifi
	$(INSTALL_BIN) ./files/firmware.sh $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/91_load_wifi.sh $(1)/lib/preinit/
endef

$(eval $(call BuildPackage,mt_wifi))
