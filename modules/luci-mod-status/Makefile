#
# Copyright (C) 2008-2014 The LuCI Team <luci@lists.subsignal.org>
#
# This is free software, licensed under the Apache License, Version 2.0 .
#

include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI Status Pages
LUCI_DEPENDS:=+luci-base +libiwinfo +rpcd-mod-iwinfo

PKG_RELEASE:=2
PKG_BUILD_DEPENDS:=iwinfo
PKG_LICENSE:=Apache-2.0

define Package/luci-mod-status/install
	# 调用父级安装方法
	$(call Package/luci-base/install,$(1))
	
	# 安装编译信息文件到固件
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) $(TOPDIR)/compile_date.txt $(1)/etc/compile_info
	
	# 修改系统状态页面JS文件
	$(SED) 's|(L\.isObject(boardinfo\.release) \? boardinfo\.release\.description + .* : .*)|fs.read("/etc/compile_info").catch(function(e){return "Custom Build";})|' \
		$(1)/htdocs/luci-static/resources/view/status/10_system.js
	
	# 确保文件权限正确
	chmod 644 $(1)/etc/compile_info
endef

include ../../luci.mk

# call BuildPackage - OpenWrt buildroot signature

