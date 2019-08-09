The code is experimental and not maintained as the same degree as our other projects.

The QEMU with RISCV hypervisor extenstion:
[https://github.com/alistair23/qemu/tree/mainline/alistair/riscv-hyp-ext-v0.3.next]

The RISCV GCC toolchain:
[https://github.com/riscv/riscv-gnu-toolchain]

You can also use the seL4 docker image [https://docs.sel4.systems/Docker.html] for the building environment.

Run the following commands after repo sync:

```console
mkdir bld
cd bld
../init-build.sh -DPLATFORM=spike -DRISCV64=1
ninja
cp ../projects/sel4_riscv_vmm/run.sh ./
./run.sh
```

The login is `root/root`.
