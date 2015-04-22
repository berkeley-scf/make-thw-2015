# default rule is the first one
algo: vec1.h base.h vec1.o vecMain.o
	g++ -o algo vec1.o vecMain.o

vec1.o: vec1.h base.h vec1.cpp
	g++ -c -o vec1.o vec1.cpp

vecMain.o: vecMain.cpp
	g++ -c -o vecMain.o vecMain.cpp
