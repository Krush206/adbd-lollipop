# Copyright 2008 The Android Open Source Project
#
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
LOCAL_MODULE := libmincrypt
LOCAL_SRC_FILES := dsa_sig.c p256.c p256_ec.c p256_ecdsa.c rsa.c sha.c sha256.c
LOCAL_CFLAGS := -Wall -Werror
include $(BUILD_STATIC_LIBRARY)

include $(CLEAR_VARS)
LOCAL_MODULE := libmincrypt.a
LOCAL_SRC_FILES := dsa_sig.c p256.c p256_ec.c p256_ecdsa.c rsa.c sha.c sha256.c
LOCAL_CFLAGS := -Wall -Werror
OBJS := $(LOCAL_SRC_FILES:.c=.o)
include $(BUILD_HOST_STATIC_LIBRARY)

all: $(LOCAL_MODULE)

%.o: %.c
	arm-linux-gnueabihf-gcc $(LOCAL_CFLAGS) -c -I../include -DHAVE_PTHREADS -o $@ $<

$(LOCAL_MODULE): $(OBJS)
	ar rcs $@ $?
	ranlib $@

clean:
	rm -f $(LOCAL_MODULE) *.o
