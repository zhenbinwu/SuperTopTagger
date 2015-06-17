IDIR       = inc
ODIR       = obj
SDIR       = src

CXX       = ~/.vim/bundle/ClangComplete/bin/cc_args.py g++
#CXX        = g++

CXXFLAGS  += -Iinc -std=c++0x 
## Optimization flag
#CXXFLAGS += -g #-O3
## Enable the maximun warning
#CXXFLAGS += -Wall -Wextra -Weffc++ -g

## Include ROOT
CXXFLAGS  += $(shell root-config --cflags)
CXXFLAGS  += -I../..
#CXXDEPFLAGS = -MMD -MP

LD         = g++
LDFLAGS    =

LIBS       = $(shell root-config --glibs)  -L../../recipeAUX/OxbridgeMT2/.libs -loxbridgekinetics-1.0 

#============================================================================#
#-----------------------------   Include Boost   ----------------------------#
#============================================================================#
ifneq ($(shell echo $(BOOSTROOT)), '')
  CXXFLAGS  += -I$(shell echo $(BOOSTROOT))
endif

PROGRAMS = testMain
PROGRAM = testMain

TOOLS =  $(ODIR)/HistTool.o    $(ODIR)/RootTools.o   

all: $(PROGRAMS)

$(ODIR)/%.o : $(SDIR)/%.C
	$(CXX) $(CXXFLAGS) $(CXXDEPFLAGS) -o $@ -c $<

$(ODIR)/%.o : $(SDIR)/%.cc
	$(CXX) $(CXXFLAGS) $(CXXDEPFLAGS) -o $@ -c $<

$(ODIR)/%.o : $(IDIR)/%.C
	$(CXX) $(CXXFLAGS) $(CXXDEPFLAGS) -o $@ -c $<

$(ODIR)/%.o : $(IDIR)/%.cc
	$(CXX) $(CXXFLAGS) $(CXXDEPFLAGS) -o $@ -c $<

tupleTest: $(ODIR)/NTupleReader.o  $(ODIR)/tupleReadTest.o
	$(LD) $^ $(LIBS)  -o $@


testMain: $(TOOLS) $(ODIR)/testMain.o  $(ODIR)/NTupleReader.o    $(ODIR)/TopTaggerAna.o
	$(LD) $^ $(LIBS)  -o $@

#$(PROGRAM):     $(OBJS)
	#@echo "Linking $(PROGRAM) ..."
	#@$(LD) $(OBJS) $(LIBS) -o $(PROGRAM)
	#@echo "done"

clean:
	rm -f $(ODIR)/*.o $(ODIR)/*.d $(PROGRAMS) core AutoDict_vector*