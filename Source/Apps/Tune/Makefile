.DEFAULT_GOAL := all

TOOLS=../../../Tools
APPBIN=../../../Binary/Apps

TASMDIR=$(TOOLS)/tasm32
TASMCMD=TASMTABS=$(TASMDIR)/ wine $(TASMDIR)/TASM.EXE


Tune.com:
	$(TASMCMD) -t180 -g3 -fFF Tune.asm Tune.com Tune.lst
	
all: Tune.com
	cp -f *.com $(APPBIN)/

clean:
	rm -f *.lst
	rm -f *.com
