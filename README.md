
The QEMU with RISCV hypervisor extenstion:

Run the following commands after repo sync:

```console
mkdir bld
cd bld
../init-build.sh -DPLATFORM=spike -DRISCV64=1
ninja
cp ../projects/sel4_riscv_vmm/run.sh ./
./run.sh
```
