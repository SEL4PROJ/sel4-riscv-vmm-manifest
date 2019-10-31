The code is experimental and not maintained as the same degree as our other projects.

Update:

31/10/19

The QEMU RISCV HE v0.4 and v0.3 working with the VMM can be downloaded from

<https://github.com/yyshen/qemu-alistair23/tree/mainline/alistair/riscv-hyp-ext-v0.4.next>

<https://github.com/yyshen/qemu-alistair23/tree/mainline/alistair/riscv-hyp-ext-v0.3.next>

They are snapshots of the original repo <https://github.com/alistair23/qemu>, which removed the
v0.3 branch.


30/10/19

master.xml is added to track the current development.
* The kernel now supports RISCV HE v0.4.
* Experimental SMP VM support is added to the VMM.

Execute
```console
repo init -u https://github.com/SEL4PROJ/sel4-riscv-vmm-manifest.git -m master.xml
repo sync
```
to use the master.xml.

To select the RISCV HE v0.4 with SMP support
```console
mkdir bld
cd bld
../init-build.sh -DPLATFORM=spike -DRISCV64=1
ccmake .
```
In the config menu:
* set `KernelRiscvHVersion` to `4` to enable V0.4 support.
* set `SMP` to `ON` to enable SMP support.
* set `KernelMaxNumNodes` to `2`, `3`, or `4` to specify the number of cores supported.
This option is also used to specify the number of VCPUs of an SMP VM.

Having chosen the values, press key `c` then `g` to generate save the new configuration.
Then, execute the following commands to build and run the VM.

```console
ninja
cp ../projects/sel4_riscv_vmm/run_smp.sh ./
./run_smp.sh
```

The QEMU RISCV HE v0.4 is from:

[https://github.com/alistair23/qemu/tree/mainline/alistair/riscv-hyp-ext-v0.4.next]


The QEMU with RISCV hypervisor extenstion v0.3:

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
