PROJECTNAME = libdeepdive
TARGET = $(PROJECTNAME).bundle

GNU =

COPS = -Wall -O2  -I. -I/usr/local/include
CPPOPS = -Wall -O2 -std=c++11 -nostdlib -nostartfiles -ffreestanding -DTARGET_CPP -fno-exceptions -fno-rtti
QPUASMOPS = --exportentry=false

LINKOPS = -dynamiclib -L/usr/local/lib -lusb-1.0 -lpthread -lz -lm -flto -g
#-lfplib
#-lgcc

COBJECTS = $(patsubst %.c, %.o, $(wildcard *.c))
CPPOBJECTS = $(patsubst %.cpp, %.o, $(wildcard *.cpp))
SOBJECTS = $(patsubst %.s, %.o, $(wildcard *.s))
QPUOBJECTS = $(patsubst %.qpuasm, %.qpuasm.h, $(wildcard *.qpuasm))

rebuild : clean build

build : $(TARGET)

clean :
	rm -f *.o


%.o : %.s
	@echo compiling as $<
	$(GNU)as $< -o $@

%.o : %.c
	@echo compiling gcc $<
	$(GNU)gcc $(COPS) -c $< -o $@

%.o : %.cpp
	@echo compiling g++ $<
	$(GNU)g++ $(CPPOPS) -c $< -o $@


$(TARGET) : $(QPUOBJECTS) $(SOBJECTS) $(COBJECTS) $(CPPOBJECTS)
	@echo $(QPUOBJECTS)
	@echo $(SOBJECTS)
	@echo $(COBJECTS)
	@echo $(CPPOBJECTS)
	$(GNU)gcc $(LINKOPS) $^ -o $@
