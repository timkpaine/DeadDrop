#===================================================================
#
# Makefile
# --------
# Makefile for building sha256 wmem, core top and wishbone
# simulations.
#
#
# Author: Joachim Strombergson
# Copyright (c) 2014, SUNET
# 
# Redistribution and use in source and binary forms, with or 
# without modification, are permitted provided that the following 
# conditions are met: 
# 
# 1. Redistributions of source code must retain the above copyright 
#    notice, this list of conditions and the following disclaimer. 
# 
# 2. Redistributions in binary form must reproduce the above copyright 
#    notice, this list of conditions and the following disclaimer in 
#    the documentation and/or other materials provided with the 
#    distribution. 
# 
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS 
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT 
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS 
# FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE 
# COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, 
# INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, 
# BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
# LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER 
# CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, 
# STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF 
# ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
#===================================================================

WMEM_SRC=./rtl/sha256_w_mem.v
WMEM_TB_SRC=./tb/tb_sha256_w_mem.v

CORE_SRC=./rtl/sha256_core.v ./rtl/sha256_k_constants.v ./rtl/sha256_w_mem.v
CORE_TB_SRC=./tb/tb_sha256_core.v

TOP_SRC=./rtl/sha256.v $(CORE_SRC)
TOP_TB_SRC=./tb/tb_sha256.v

INST_TB_SRC=./tb/sha_tb.sv

#CC=iverilog
CC=vcs
FLAGS=-full64 -PP -sverilog +define+SV +define+VPD -notice

instrument:$(INST_TB_SRC) $(TOP_SRC)
	$(CC) $(FLAGS) -o instrument.sim $(INST_TB_SRC) $(TOP_SRC)


all: top core wmem


top: $(TOP_TB_SRC) $(TOP_SRC)
	$(CC) $(FLAGS) -o top.sim $(TOP_TB_SRC) $(TOP_SRC)


core: $(CORE_TB_SRC) $(CORE_SRC)
	$(CC) $(FLAGS) -o core.sim $(CORE_SRC) $(CORE_TB_SRC)


wmem: $(WMEM_SRC) $(WMEM_TB_SRC)
	$(CC) $(FLAGS) -o wmem.sim $(WMEM_SRC) $(WMEM_TB_SRC)


sim-top: top.sim
	./top.sim


sim-core: core.sim
	./core.sim


sim-wmem: wmem.sim
	./wmem.sim


debug:
	@echo "No debug available."


clean:
	rm -f top.sim
	rm -f core.sim
	rm -f wmem.sim
	rm -f instrument.sim
	rm -rf *.o *~ *.vcd *.vpd sim* csrc DVEfiles *daidir *.ver *.exe *.exe.vdb *.key vc_hdrs.h urgReport


help:
	@echo "Supported targets:"
	@echo "------------------"
	@echo "all:      Build all simulation targets."
	@echo "top:      Build the top simulation target."
	@echo "core:     Build the core simulation target."
	@echo "wmem:     Build the wmem simulation target."
	@echo "sim-top:  Run top level simulation."
	@echo "sim-core: Run core level simulation."
	@echo "sim-wmem: Run wmem level simulation."
	@echo "debug:    Print the internal varibles."
	@echo "clean:    Delete all built files."

#===================================================================
# EOF Makefile
#===================================================================

