PROJ = example
PIN_DEF = ice40hx8k-evb.pcf
DEVICE = hx8k

all: $(PROJ).rpt $(PROJ).bin

%.json: %.v
	yosys -p 'synth_ice40 -top top -json $@' $<

%.asc:  $(PIN_DEF) %.json
	nextpnr-ice40  --hx8k --json $*.json --asc $@ --pcf $< --pcf-allow-unconstrained --package ct256

%.bin: %.asc
	icepack $< $@

%.rpt: %.asc
	icetime -d $(DEVICE) -mtr $@ $<

prog: $(PROJ).bin
	sudo iceprogduino $<

sudo-prog: $(PROJ).bin
	@echo 'Executing prog as root!!!'
	sudo iceprogduino $<


.PHONY: all prog 
