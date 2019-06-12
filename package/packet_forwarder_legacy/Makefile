# Author: Daniel Knox <d.knox@kent.ac.uk>

include $(TOPDIR)/rules.mk

PKG_NAME:=lora_packet_forwarder_legacy
PKG_VERSION:=1.2
PKG_RELEASE:=v0.1.0

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nhanlee97/picoGW_packet_forwarder.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=8176124e5c38174715b3ba2b21f619c7190fd435
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/lora_packet_forwarder_legacy_pico
  TITLE:=Lora Packet Forwarder Legacy
	DEPENDS:=+lora_gateway_pico
	SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Lora
endef

define Package/lora_packet_forwarder_legacy_pico/description
	LoRa Packet forwarder for Linux based gateways
endef

TARGET_CFLAGS += $(FPIC) -O2 -Wall -Wextra -std=c99 -Iinc -I.

define Package/lora_packet_forwarder_legacy_pico/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lora_pkt_fwd/lora_pkt_fwd $(1)/usr/bin
	$(INSTALL_BIN) ./files/pktinit.sh $(1)/usr/bin/pktinit.sh
	$(INSTALL_DIR) $(1)/etc/lora
	$(INSTALL_CONF) ./files/conf/*.json $(1)/etc/lora/
	$(INSTALL_CONF) ./files/local_conf.json $(1)/usr/bin/local_conf.json
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/lora-global.config $(1)/etc/config/lora-global
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/lora_pkt_fwd.init $(1)/etc/init.d/lora_pkt_fwd

endef

$(eval $(call BuildPackage,lora_packet_forwarder_legacy_pico))
