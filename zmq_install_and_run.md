###########################
build libzmq static for emscripten:
	 cd libzmq
	emconfigure ./autorun.sh
	emconfigure ./configure --enable-static
	emmake make 
	sudo make install 
	ldconfig 
	copy .a , .bc, .so , .so.1.4(rename this one into .bc extn) to pwd

###########################
steps to complie zmq on emscripten: libzmq

1. Move the complied static library to pwd. Rename the so.1.5 file to .bc 
2. compile cpp source into object file
emcc -c -o tmp1.o -s WASM=1 -s NO_EXIT_RUNTIME=0 -s EXPORTED_FUNCTIONS="['_main',_zmq_version]" zmqtest.cpp -I/usr/local/include 
3. complie object into js/html by linking .o and .bc file.
emcc -o tmp2.o -s WASM=1 -s NO_EXIT_RUNTIME=0  libzmq.bc -I/usr/local/include
4.run your project on browser.

############################
