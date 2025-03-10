# Copyright 2005 The Android Open Source Project
#
# Android.mk for adb
#

# adbd device daemon
# =========================================================

include $(CLEAR_VARS)

LOCAL_SRC_FILES := \
	adb.c \
	fdevent.c \
	transport.c \
	transport_local.c \
	transport_usb.c \
	adb_auth_client.c \
	sockets.c \
	services.c \
	file_sync_service.c \
	jdwp_service.c \
	framebuffer_service.c \
	remount_service.c \
	usb_linux_client.c

LOCAL_CFLAGS := -O2 -g -DADB_HOST=0 -Wall -Wno-unused-parameter -DPROP_NAME_MAX=32 -DPROP_VALUE_MAX=92
LOCAL_CFLAGS += -D_XOPEN_SOURCE -D_GNU_SOURCE -DALLOW_ADBD_ROOT=1 -DHAVE_PTHREADS

ifneq (,$(filter userdebug eng,$(TARGET_BUILD_VARIANT)))
LOCAL_CFLAGS += -DALLOW_ADBD_ROOT=1
endif

LOCAL_MODULE := adbd

LOCAL_FORCE_STATIC_EXECUTABLE := true
LOCAL_MODULE_PATH := $(TARGET_ROOT_OUT_SBIN)
LOCAL_UNSTRIPPED_PATH := $(TARGET_ROOT_OUT_SBIN_UNSTRIPPED)

LOCAL_STATIC_LIBRARIES := liblog libcutils libc libmincrypt libselinux
OBJS := $(LOCAL_SRC_FILES:.c=.o)
include $(BUILD_EXECUTABLE)


all: $(LOCAL_MODULE)

%.o: %.c
	arm-linux-gnueabihf-gcc $(LOCAL_CFLAGS) -c -I../include -I. -o $@ $<

$(LOCAL_MODULE): $(OBJS)
	arm-linux-gnueabihf-gcc -static -o adbd -L../libcutils -L../liblog -L../libmincrypt $^ -lcutils -llog -lmincrypt -lresolv

clean:
	rm -f $(LOCAL_MODULE) *.o
