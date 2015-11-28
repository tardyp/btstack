# lipoplastic setup for armv6 + arm64 compilation
TARGET := iphone:clang
THEOS_PLATFORM_SDK_ROOT_armv6 = /Applications/Xcode-4.4.1.app/Contents/Developer
SDKVERSION_armv6 = 5.1
TARGET_IPHONEOS_DEPLOYMENT_VERSION = 3.0
TARGET_IPHONEOS_DEPLOYMENT_VERSION_arm64 = 7.0
ARCHS = armv6 arm64

BTSTACK_ROOT=../../..

VPATH += $(BTSTACK_ROOT)/src \
		 $(BTSTACK_ROOT)/src/classic \
		 $(BTSTACK_ROOT)/platform/posix/src \
		 $(BTSTACK_ROOT)/platform/daemon/src \
		 $(BTSTACK_ROOT)/platform/cocoa \
		 $(BTSTACK_ROOT)/port/ios/SpringBoardAccess

LIBRARY_NAME = libBTstack
libBTstack_FILES = \
	daemon_cmds.c \
	hci_cmds.c \
	hci_dump.c \
	linked_list.c \
	run_loop.c \
	sdp_util.c \
	utils.c \
	run_loop_cocoa.m \
	run_loop_posix.c \
	btstack.c \
	socket_connection.c \

libBTstack_CFLAGS = -I$(BTSTACK_ROOT)/src/ble -I$(BTSTACK_ROOT)/src -I..

TOOL_NAME = BTdaemon
BTdaemon_FILES = \
	$(libBTstack_FILES)  	\
	btstack_memory.c        \
	hci.c                   \
	l2cap.c                 \
	l2cap_signaling.c       \
	memory_pool.c           \
	rfcomm.c                \
	sdp.c                   \
    sdp_client.c            \
    sdp_parser.c            \
    sdp_query_rfcomm.c      \
    sdp_query_util.c        \
	daemon.c  				    \
	hci_transport_h4.c 		 	\
	bt_control_iphone.m     	\
	hci_transport_h4_iphone.c   \
	platform_iphone.m       	\
	SpringBoardAccess.c         \
	remote_device_db_cocoa.m  	\

BTdaemon_CFLAGS = -I$(BTSTACK_ROOT)/src -I$(BTSTACK_ROOT)/platform/daemon/src -I..
BTdaemon_PRIVATE_FRAMEWORKS = IOKIT

before-all::
	../../../tool/get_version.sh

after-BTdaemon-stage::
	echo $(THEOS_STAGING_DIR)
	mkdir -p ../.theos/_/usr/local/lib
	mkdir -p ../.theos/_/usr/local/bin
	ln -s /usr/lib/libBTstack.dylib ../.theos/_/usr/local/lib
	ln -s /usr/bin/BTdaemon         ../.theos/_/usr/local/bin/BTdaemon

include $(THEOS)/makefiles/common.mk
include $(THEOS_MAKE_PATH)/library.mk
include $(THEOS_MAKE_PATH)/tool.mk