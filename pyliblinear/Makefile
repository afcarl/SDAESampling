CXX ?= g++
CC ?= gcc
CFLAGS = -Wall -Wconversion -O3 -fPIC
LIBS = blas/blas.a
SHVER = 1
#LIBS = -lblas

all: train predict run_all tron.o lib linear.o blas/blas.a

lib: linear.o tron.o blas/blas.a
	$(CXX) -shared -dynamiclib linear.o tron.o blas/blas.a -o liblinear.so.$(SHVER)

train: tron.o linear.o train.c blas/blas.a
	$(CXX) $(CFLAGS) -o train train.c tron.o linear.o $(LIBS)

predict: tron.o linear.o predict.c blas/blas.a
	$(CXX) $(CFLAGS) -o predict predict.c tron.o linear.o $(LIBS)

run_all: tron.o linear.o runAll.cpp blas/blas.a
	$(CXX) $(CFLAGS) -o run_all runAll.cpp tron.o linear.o $(LIBS)

tron.o: tron.cpp tron.h
	$(CXX) $(CFLAGS) -c -o tron.o tron.cpp

linear.o: linear.cpp linear.h
	$(CXX) $(CFLAGS) -c -o linear.o linear.cpp

blas/blas.a:
	cd blas; make OPTFLAGS='$(CFLAGS)' CC='$(CC)';

clean:
	cd blas;	make clean
	cd matlab;	make clean
	rm -f *~ tron.o linear.o train predict run_all liblinear.so.$(SHVER)
