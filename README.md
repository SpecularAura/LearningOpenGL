## Makefile For Reference
```
CC = g++
CC_FLAGS = -g -std=c++17

IDIRGLFW = ../../dependencies/GLFW/include
IDIRGlad = ../../dependencies/Glad/include
IDIR = ../../dependencies/Headers 

INCLUDE = -I$(IDIR) -I$(IDIRGLFW) -I$(IDIRGlad) 

LIBDIR = ../../dependencies/GLFW/lib-mingw-w64
LIBS = -L$(LIBDIR)

LIBLINK = -lopengl32 -lglfw3 -lgdi32 #-mwindows
#_DEPS = testinclude.h
_DEPS = $(wildcard $(IDIR)/*.h)
#DEPS = $(patsubst %,$(IDIR)/%,$(_DEPS))
DEPS = $(_DEPS)

SRCDIR = ../../dependencies/Source_code
ODIR = ../../dependencies/Objects
#_CPP = testinclude.cpp
_CPP = $(wildcard $(SRCDIR)/*.cpp)
#CPP = $(patsubst %,$(SRCDIR)/%,$(_CPP))
CPP = $(_CPP)

#_OBJ = $(patsubst %.cpp,%.o,$(CPP))
_OBJ = $(patsubst $(SRCDIR)/%.cpp,$(ODIR)/%.o,$(CPP))
OBJ = $(_OBJ) ${ODIR}/glad.o 
EXECUTABLE = main

$(EXECUTABLE):glad.o $(OBJ)
	$(CC) $(CC_FLAGS) src/$@.cpp $(INCLUDE) $(LIBS) $(OBJ) -o $@ $(LIBLINK)

$(ODIR)/%.o:$(SRCDIR)/%.cpp $(DEPS) 
	$(CC) $(CC_FLAGS) -c $< $(INCLUDE)  -o $@

glad.o:
	gcc -c ../../dependencies/Source_code/glad.c -I../../dependencies/Glad/include -o ../../dependencies/Objects/glad.o
```
