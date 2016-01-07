include $(TOPDIR)/rules.mk

PKG_NAME:=qcam
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_BUILD_PARALLEL:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/OpenQCam/openqcam.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=208f6b68d67451b55c8f76dbe0aa0cc4bf0fb183
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  CATEGORY:=QIC1832 SDK
  TITLE:=Streaming QIC1832 camera video to client over RTSP/RTMP.
  URL:=
  DEPENDS:= \
  	+qic1832_sdk \
	+libstdcpp \
	+@CONFIG_LIBCURL_COOKIES \
	+@CONFIG_LIBCURL_FILE \
	+@CONFIG_LIBCURL_FTP \
	+@CONFIG_LIBCURL_HTTP \
	+@CONFIG_LIBCURL_NO_SMB \
	+@CONFIG_LIBCURL_POLARSSL \
	+@CONFIG_LIBCURL_PROXY \
	+@CONFIG_OPENSSL_WITH_EC \
	+alsa-lib \
	+iperf \
	+kmod-input-core \
	+kmod-sound-core \
	+kmod-usb-audio \
	+kmod-usb-uhci \
	+kmod-video-core \
	+kmod-video-uvc \
	+kmod-video-videobuf2 \
	+libcurl \
	+libiwinfo-lua \
	+liblua \
	+libopenssl \
	+libpolarssl \
	+libpthread \
	+libreadline \
	+librt \
	+libubus-lua \
	+libuci-lua \
	+libustream-polarssl \
	+lua \
	+luci \
	+luci-app-firewall \
	+luci-base \
	+luci-lib-ip \
	+luci-lib-nixio \
	+luci-mod-admin-full \
	+luci-proto-ipv6 \
	+luci-proto-ppp \
	+luci-ssl \
	+luci-theme-bootstrap \
	+px5g \
	+rpcd \
	+uclibcxx \
	+uhttpd \
	+uhttpd-mod-ubus \
	+zlib
  	
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

