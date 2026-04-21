SPK_NAME = rr-manager
SPK_VERS = 4.0
SPK_REV = 7
SPK_ICON = src/rr-manager.png

override ARCH = noarch

MAINTAINER = RROrg
DESCRIPTION = Manage RR bootloader configuration and RR upgrades directly from DSM.
DISPLAY_NAME = RR Manager
HOMEPAGE = https://github.com/RROrg/rr
LICENSE = GPLv3

DSM_UI_DIR = ui
DSM_UI_CONFIG = src/ui/config
DSM_APP_NAME = RROrg.RRManager.Application

CONF_DIR = src/conf
SYSTEM_GROUP = http
SERVICE_SETUP = src/service-setup.sh
SSS_SCRIPT = src/start-stop-status.sh
STARTABLE = no
COPY_TARGET = nop
POST_STRIP_TARGET = rr_manager_extra_install

UI_HTML_FILES = $(notdir $(wildcard src/ui/*.html))
TEXT_LANGS = $(notdir $(wildcard src/ui/texts/*))
HELP_LANGS = $(notdir $(wildcard src/ui/help/*))

include ../../mk/spksrc.common.mk
include ../../mk/spksrc.spk.mk

.PHONY: rr_manager_extra_install
rr_manager_extra_install:
	install -m 755 -d $(STAGING_DIR)/ui
	install -m 755 -d $(STAGING_DIR)/bin
	install -m 755 -d $(STAGING_DIR)/var
	install -m 755 -d $(STAGING_DIR)/ui/images
	install -m 755 -d $(STAGING_DIR)/ui/scripts
	for lang in $(TEXT_LANGS); do \
		install -m 755 -d $(STAGING_DIR)/ui/texts/$$lang; \
	done
	for lang in $(HELP_LANGS); do \
		install -m 755 -d $(STAGING_DIR)/ui/help/$$lang; \
	done

	install -m 644 src/ui/config $(STAGING_DIR)/ui/config
	install -m 644 src/ui/application.cfg $(STAGING_DIR)/ui/application.cfg
	install -m 644 src/ui/index.conf $(STAGING_DIR)/ui/index.conf
	install -m 644 src/ui/helptoc.conf $(STAGING_DIR)/ui/helptoc.conf
	install -m 644 src/ui/style.css $(STAGING_DIR)/ui/style.css
	install -m 644 src/ui/app.js $(STAGING_DIR)/ui/app.js
	install -m 644 src/ui/rr-manager.js $(STAGING_DIR)/ui/rr-manager.js
	install -m 644 $(addprefix src/ui/,$(UI_HTML_FILES)) $(STAGING_DIR)/ui/
	install -m 755 src/ui/scripts/api.cgi $(STAGING_DIR)/ui/scripts/api.cgi
	for lang in $(HELP_LANGS); do \
		install -m 644 src/ui/help/$$lang/index.html $(STAGING_DIR)/ui/help/$$lang/index.html; \
	done
	for lang in $(TEXT_LANGS); do \
		install -m 644 src/ui/texts/$$lang/strings $(STAGING_DIR)/ui/texts/$$lang/strings; \
		install -m 644 src/ui/texts/$$lang/ui.json $(STAGING_DIR)/ui/texts/$$lang/ui.json; \
	done
	install -m 644 src/ui/images/*.png $(STAGING_DIR)/ui/images/

	install -m 755 src/bin/rr-manager-lib.sh $(STAGING_DIR)/bin/rr-manager-lib.sh
	install -m 755 src/bin/rr-manager-job.sh $(STAGING_DIR)/bin/rr-manager-job.sh
