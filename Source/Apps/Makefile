.DEFAULT_GOAL := all

TOOLS=../../Tools
APPBIN=../../Binary/Apps

TASMDIR=$(TOOLS)/tasm32
TASMCMD=TASMTABS=$(TASMDIR)/ wine $(TASMDIR)/TASM.EXE
ZXCMD=ZXBINDIR=$(TOOLS)/cpm/bin/ ZXLIBDIR=$(TOOLS)/cpm/lib/ ZXINCDIR=$(TOOLS)/cpm/include/ wine $(TOOLS)/zx/zx.exe

COMFILES=SysCopy.com Assign.com Format.com Talk.com OSLdr.com Mode.com RTC.com Timer.com

#
#

sysgen.com:
	$(ZXCMD) Z80ASM -SYSGEN/F

survey.com: 
	$(ZXCMD) MAC SURVEY.ASM -$PO
	$(ZXCMD) MLOAD25 -SURVEY.COM=SURVEY.HEX

IntTest.com: IntTest.asm
	$(TASMCMD) -t180 -g3 -fFF $^ $@ $(addsuffix .lst, $(basename $^))


FDU.com:
	cd FDU && $(MAKE) all

Tune.com:
	cd Tune && $(MAKE) all

XM.com:
	cd XM && $(MAKE) all

%.com: %.asm 	
	$(TASMCMD) -t80 -g3 -fFF $^ $@ $(addsuffix .lst, $(basename $^))

all: $(COMFILES) sysgen.com survey.com FDU.com IntTest.com Tune.com XM.com
	cp -f *.com $(APPBIN)/

clean:
	rm -f *.bin
	rm -f *.com
	rm -f *.lst
	rm -f *.hex
	rm -f *.prn
	cd FDU && $(MAKE) clean
	cd Tune && $(MAKE) clean
	cd XM && $(MAKE) clean


