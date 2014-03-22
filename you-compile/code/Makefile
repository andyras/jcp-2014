# ---- variables for building ---- #

# directories for headers, objects and source files
INCDIR = include
OBJDIR = obj
SRCDIR = src

# ---- [DO NOT CHANGE] base flags ---- #
LDFLAGS = -lsundials_cvode -lsundials_nvecserial
INCLUDES =
CXXFLAGS = -O3 -xHOST -no-prec-div -Wall -std=c++11 -no-multibyte-chars
CXXFLAGS =

# ---- [CHANGE] compiler-specific flags ---- #
# --- Intel compiler --- #
CXX = icpc
CXXFLAGS += -fopenmp
LDFLAGS += -mkl

# --- GCC --- #
#CXX = g++
#CXXFLAGS +=
#LDFLAGS += -llapack

# name of main executable
### This line should be just about all you have to change ###
BIN = dynamix
#############################################################

CXXFLAGS = -O3 -Wall
CXXFLAGS = -Wall
INCLUDES = -I./$(INCDIR)

# make will look for .cpp files in $(SRCDIR)
vpath %.cpp $(SRCDIR)

# list of source files
SOURCES = $(wildcard $(SRCDIR)/*.cpp)

# object files have same name as .cpp files, but with .o extension
OBJECTS = $(patsubst $(SRCDIR)/%.cpp,obj/%.o,$(SOURCES))

# ---- build rules ---- #

# build the main executable; this should be listed first
$(BIN): $(OBJECTS)
	$(CXX) -o $@ $^ $(LDFLAGS) $(INCLUDES)

# automatic rule for building objects
$(OBJDIR)/%.o: %.cpp
	$(CXX) $(CXXFLAGS) $(INCLUDES) -c $< -o $@

# all objects depend on object directory
$(OBJECTS): | $(OBJDIR)

# make object directory if it does not exist
$(OBJDIR):
	mkdir -p $(OBJDIR)

.PHONY: clean

clean:
	rm -rf $(OBJDIR)
	rm -f $(BIN)