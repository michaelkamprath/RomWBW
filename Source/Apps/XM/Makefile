.DEFAULT_GOAL := all

TOOLS=../../../Tools
APPBIN=../../../Binary/Apps

ZXCMD=ZXBINDIR=$(TOOLS)/cpm/bin/ ZXLIBDIR=$(TOOLS)/cpm/lib/ ZXINCDIR=$(TOOLS)/cpm/include/ wine $(TOOLS)/zx/zx.exe

xm.com: xmdm125.asm
	$(ZXCMD) mac xmdm125.asm $PO
	$(ZXCMD) slr180 -xmhb/HF
	$(ZXCMD) mload25 XM=xmdm125,xmhb
	
all: xm.com
	cp -f *.com $(APPBIN)/
	
clean:
	rm -f *.hex
	rm -f *.prn
	rm -f *.lst
	rm -f *.com
