# (c) 2023 SAFARI Research Group at ETH Zurich, Gagandeep Singh, D-ITET   
  
# This file is licensed under the Apache License v2.0 with LLVM Exceptions.
# See https://llvm.org/LICENSE.txt for license information.
# SPDX-License-Identifier: Apache-2.0 WITH LLVM-exception

ACDC_AIE = $(dir $(shell which aie-opt))/..
ACDC_AIR = $(dir $(shell which air-opt))/..
SYSROOT = /mnt/scratch/gagsingh/sysroot/sysroot

i32: i32_chess i32.elf
f32: f32_chess f32.elf

build: 
	/mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/bin/xchessmk test.prx
sim: 
	xca_udm_dbg -P /mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/data/cervino/lib/ -t sim.tcl


i32_chess: 
	/mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/bin/xchesscc -p me -P /mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/data/cervino/lib/ -L /mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/data/cervino/lib/ -c ./hdiff_lap.cc ./hdiff_flux1.cc ./hdiff_flux2.cc

f32_chess: 
	/mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/bin/xchesscc -p me -P /mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/data/cervino/lib/ -L /mnt/scratch/tools_tmp/Xilinx/Vitis/2021.2/aietools/data/cervino/lib/ -c ./hdiff_lap_fp32.cc ./hdiff_flux1_fp32.cc ./hdiff_flux2_fp32.cc

i32.elf: 
	/mnt/scratch/gagsingh/mlir-aie/install/bin/aiecc.py --sysroot=/mnt/scratch/gagsingh/sysroot/sysroot --host-target=aarch64-linux-gnu aie_$(b).mlir \
	-I/mnt/scratch/gagsingh/mlir-aie/install/runtime_lib /mnt/scratch/gagsingh/mlir-aie/install/runtime_lib/test_library.cpp ./test_$(b).cpp -o test_$(b).elf


f32.elf: 
	/mnt/scratch/gagsingh/mlir-aie/install/bin/aiecc.py --sysroot=/mnt/scratch/gagsingh/sysroot/sysroot --host-target=aarch64-linux-gnu aie_fp32.mlir \
	-I/mnt/scratch/gagsingh/mlir-aie/install/runtime_lib /mnt/scratch/gagsingh/mlir-aie/install/runtime_lib/test_library.cpp ./test.cpp -o test.elf

clean:
	rm -rf work *mem acdc_project core_* test.elf *.o

