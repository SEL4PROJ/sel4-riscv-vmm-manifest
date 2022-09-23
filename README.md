Note: The code is experimental and not maintained as the same degree as our other projects.

The VMM supports v0.6.1 of the RISC-V Hypervisor Extension.

## Getting the code
```console
repo init -u https://github.com/SEL4PROJ/sel4-riscv-vmm-manifest.git -m master.xml
repo sync
```

## Building and running

You can either build and run the using the seL4 Docker environment or build natively
on a platform that is supported by seL4.

Dependencies for building natively:
* [seL4 host dependencies](https://docs.sel4.systems/projects/buildsystem/host-dependencies.html)
* [RISC-V GNU toolchain](https://github.com/riscv/riscv-gnu-toolchain)
* RISC-V QEMU, the stable-6.0 branch from https://gitlab.com/qemu-project/qemu.git works.

### Single-core
```console
mkdir build
cd build
../init-build.sh -DPLATFORM=spike -DRISCV64=1
ninja
cp ../projects/sel4_riscv_vmm/run.sh ./
./run.sh
```

### Multi-core (SMP)
```console
mkdir build
cd build
../init-build.sh -DPLATFORM=spike -DRISCV64=1 -DSMP=1 -DKernelMaxNumNodes=<NUM_NODES>
ninja
cp ../projects/sel4_riscv_vmm/run_smp.sh ./
./run_smp.sh
```

The `KernelMaxNumNodes` option specifies the number of cores supported, it is also used
to specify the number of VCPUs an SMP VM uses.

You can also use `ccmake .` to open the configuration menu and change the number of
nodes from there. Press the keys `c` and then `g` to generate and save the new config.

## Building a Linux image

The Linux image is included in `projects/sel4_riscv_vmm/linux`, if you would
like build it yourself, you can use the following instructions:

```console
git clone git@github.com:SEL4PROJ/sel4-riscv-vmm-linux-5.2.git
make ARCH=riscv CROSS_COMPILE=<RISCV_TOOLCHAIN_PREFIX> sel4vm_defconfig all
```

If you would like to build an image for the multi-core VMM instead, you'll need to change
the config. You can enter the menuconfig by executing:

```console
make ARCH=riscv CROSS_COMPILE=<RISCV_TOOLCHAIN_PREFIX> sel4vm_defconfig menuconfig
```

From here you need to go to the "Platform type" section and turn on "Symmetric Multi-Processing",
and configure the maximum number of CPUs you want.

The configuration will be written to `.config`. To build:
```console
make ARCH=riscv CROSS_COMPILE=<RISCV_TOOLCHAIN_PREFIX> .config all
```

You'll find the image in `arch/riscv/boot`. It'll need to replace the image as `linux`
for single-core, and `linux-smp` for multi-core in `projects/sel4_riscv_vmm/linux/`.
