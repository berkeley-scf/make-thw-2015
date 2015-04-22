# set prefix only if not already set (i.e., this provides a default value)
prefix ?= /usr/local/magma

bin:
        cd bin && $(MAKE)

lib:
	@echo ======================================== magmablas
	( cd magmablas      && $(MAKE) )
	@echo ======================================== src
	( cd src            && $(MAKE) )
	@echo ======================================== control
	( cd control        && $(MAKE) )
	@echo ======================================== interface
	( cd interface_cuda && $(MAKE) )

dir:
	mkdir -p $(prefix)
	mkdir -p $(prefix)/bin
	mkdir -p $(prefix)/include
	mkdir -p $(prefix)/lib
	mkdir -p $(prefix)/lib/pkgconfig

install: bin lib dir
	cp $(MAGMA_DIR)/include/*.h  $(prefix)/include
	cp $(LIBMAGMA)               $(prefix)/lib
	-cp $(LIBMAGMA_SO)           $(prefix)/lib
        cp $(BINARY}                 $(prefix)/bin
