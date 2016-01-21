include $(TOPDIR)/rules.mk

PKG_NAME:=qcam
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_BUILD_PARALLEL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/OpenQCam/qcam.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=abd9a09f905b86a9bea2055cee0b9cffde93aff6
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  CATEGORY:=QIC1832 SDK
  TITLE:=Streaming QIC1832 camera video to client over RTSP/RTMP.
  DEFAULT:=y
  URL:=
  DEPENDS:= \
  	+qic1832_sdk \
	+libstdcpp \
	+libopenssl \
	+libpthread \
	+librt
  	
endef

define Build/Configure
	$(call Build/Configure/Default,--with-linux-headers=$(LINUX_DIR))
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/output/qcam $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/etc/qcam
	$(INSTALL_CONF) files/streamer.lua $(1)/etc/qcam/streamer.lua
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/trunk/builders/cmake/applications/qicstreamer/server.key $(1)/etc/qcam/server.key
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/trunk/builders/cmake/applications/qicstreamer/server.crt $(1)/etc/qcam/server.crt
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/trunk/builders/cmake/nvram_test.xml $(1)/etc/qcam/nvram_test.xml
endef

$(eval $(call BuildPackage,$(PKG_NAME)))

