.DEFAULT_GOAL := all

TOOLS=../../../Tools
APPBIN=../../../Binary/Apps

TASMDIR=$(TOOLS)/tasm32
TASMCMD=TASMTABS=$(TASMDIR)/ wine $(TASMDIR)/TASM.EXE


FDU.com:
	$(TASMCMD) -t80 -b -fFF FDU.asm FDU.com FDU.lst
	
all: FDU.com
	cp -f *.com $(APPBIN)/

clean:
	rm -f *.lst
	rm -f *.com
	rm -f *.zip
