all: respondd.so

CFLAGS += -Wall

ifeq ($(origin PKG_CONFIG), undefined)
  PKG_CONFIG = pkg-config
  ifeq ($(shell which $(PKG_CONFIG) 2>/dev/null),)
    $(error $(PKG_CONFIG) not found)
  endif
endif

ifeq ($(origin LIBNL_CFLAGS) $(origin LIBNL_LDLIBS), undefined undefined)
  LIBNL_NAME ?= libnl-tiny
  ifeq ($(shell $(PKG_CONFIG) --modversion $(LIBNL_NAME) 2>/dev/null),)
    $(error No $(LIBNL_NAME) development libraries found!)
  endif
  LIBNL_CFLAGS += $(shell $(PKG_CONFIG) --cflags $(LIBNL_NAME))
  LIBNL_LDLIBS +=  $(shell $(PKG_CONFIG) --libs $(LIBNL_NAME))
endif
CFLAGS += $(LIBNL_CFLAGS)
LDLIBS += $(LIBNL_LDLIBS)

ifeq ($(origin LIBBATADV_CFLAGS) $(origin LIBBATADV_LDLIBS), undefined undefined)
  LIBBATADV_NAME ?= libbatadv
  ifeq ($(shell $(PKG_CONFIG) --modversion $(LIBBATADV_NAME) 2>/dev/null),)
    $(error No $(LIBBATADV_NAME) development libraries found!)
  endif
  LIBBATADV_CFLAGS += $(shell $(PKG_CONFIG) --cflags $(LIBBATADV_NAME))
  LIBBATADV_LDLIBS += $(shell $(PKG_CONFIG) --libs $(LIBBATADV_NAME))
endif
CFLAGS += $(LIBBATADV_CFLAGS)
LDLIBS += $(LIBBATADV_LDLIBS)

respondd.so: respondd.c
	$(CC) $(CPPFLAGS) $(CFLAGS) $(LDFLAGS) -shared -fPIC -D_GNU_SOURCE -o $@ $^ $(LDLIBS) -lgluonutil -liwinfo -luci
