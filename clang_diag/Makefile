LLVM_CONFIG?=/home/dbhaskar/ROCm/hcc/build/compiler/bin/llvm-config
ifndef VERBOSE
	QUIET:=@
endif
CXX=clang
SRC_DIR?=$(PWD)
LDFLAGS+=$(shell $(LLVM_CONFIG) --ldflags)
COMMON_FLAGS=-Wall -Wextra -fno-rtti -I/opt/rocm/hcc/include/ -I/home/dbhaskar/ROCm/hcc/clang/include
CXXFLAGS+=$(COMMON_FLAGS) $(shell $(LLVM_CONFIG) --cxxflags)
CPPFLAGS+=$(shell $(LLVM_CONFIG) --cppflags) -I$(SRC_DIR)
CLANGLIBS = \
			-Wl,--start-group\
			-lclang\
			-lclangFrontend\
			-lclangDriver\
			-lclangSerialization\
			-lclangParse\
			-lclangSema\
			-lclangAnalysis\
			-lclangEdit\
			-lclangAST\
			-lclangLex\
			-lclangBasic\
			-Wl,--end-group


LLVMLIBS=$(shell $(LLVM_CONFIG) --libs)
PROJECT=myproject
PROJECT_OBJECTS=project.o
default: $(PROJECT)
	%.o : $(SRC_DIR)/%.cpp
	@echo Compiling $*.cpp
	$(QUIET)$(CXX) -c $(CPPFLAGS) $(CXXFLAGS) $<

$(PROJECT) : $(PROJECT_OBJECTS)
	@echo Linking $@
	$(QUIET)$(CXX) -o $@ $(CXXFLAGS) $(LDFLAGS) $^ $(CLANGLIBS)
	$(LLVMLIBS)

clean::
	$(QUIET)rm -f $(PROJECT) $(PROJECT_OBJECTS)
