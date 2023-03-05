# Makefile
# See https://docs.cocotb.org/en/stable/quickstart.html for more info

# defaults
SIM ?= icarus
TOPLEVEL_LANG ?= verilog

ifneq ($(GATES),yes)
# normal simulation
VERILOG_SOURCES += $(PWD)/tb.v $(PWD)/counter.v $(PWD)/decoder.v
else
# pick up the gatelevel verilog from /runs/wokwi/results/final/verilog/gl/
GATE_SOURCES := $(filter-out $(wildcard $(PWD)/../runs/wokwi/results/final/verilog/gl/*.nl.v), $(wildcard $(PWD)/../runs/wokwi/results/final/verilog/gl/*.v))
VERILOG_SOURCES := $(PWD)/tb.v $(GATE_SOURCES)

# gate level simulation requires some extra setup
COMPILE_ARGS    += -DGL_TEST
COMPILE_ARGS    += -DFUNCTIONAL
COMPILE_ARGS    += -DUSE_POWER_PINS
COMPILE_ARGS    += -DSIM
COMPILE_ARGS    += -DUNIT_DELAY=#1
COMPILE_ARGS    += -DSIM
VERILOG_SOURCES += $(PDK_ROOT)/sky130B/libs.ref/sky130_fd_sc_hd/verilog/primitives.v
VERILOG_SOURCES += $(PDK_ROOT)/sky130B/libs.ref/sky130_fd_sc_hd/verilog/sky130_fd_sc_hd.v
endif

# TOPLEVEL is the name of the toplevel module in your Verilog or VHDL file
TOPLEVEL = tb

# MODULE is the basename of the Python test file
MODULE = test

# include cocotb's make rules to take care of the simulator setup
include $(shell cocotb-config --makefiles)/Makefile.sim

