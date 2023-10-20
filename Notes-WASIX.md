You'll need a clang capable of targeting wasi and the wasix-libc sysroot.

simply use a command line like

```bash
RANLIB=llvm-ranlib-15 AR=llvm-ar-15 NM=llvm-nm-15 CC="clang-15 --target=wasm32-wasi" CXX="clang-15 --target=wasm32-wasi" CFLAGS="--sysroot=/home/seb/wasix-libc/sysroot32 -matomics -mbulk-memory -mmutable-globals -pthread -mthread-model posix -ftls-model=local-exec -fno-trapping-math -D_WASI_EMULATED_MMAN -D_WASI_EMULATED_SIGNAL -D_WASI_EMULATED_PROCESS_CLOCKS " LDFLAGS="-Wl,--shared-memory -Wl,--max-memory=4294967296 -Wl,--import-memory -Wl,--export-dynamic -Wl,--export=__heap_base -Wl,--export=__stack_pointer -Wl,--export=__data_end -Wl,--export=__wasm_init_tls -Wl,--export=__wasm_signal -Wl,--export=__tls_size -Wl,--export=__tls_align -Wl,--export=__tls_base" ./configure --static
```

then `make` and you'll have a wasi/wasix build of zlib.
