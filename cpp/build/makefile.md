单个文件编译

g++  xxx.cpp -c (只编译不连接)

g++ *.o -o main（把使用.o文件链接在一起）

./main

#version1

```makefile
hello: main.cpp printhello.cpp xxx.cpp ##(依赖文件)
	g++ -o main.cpp printhello.cpp xxx.cpp ##（编译）
```

修改文件后 make会重新编译

如果文件成千上万个，编写起来非常麻烦

#version2

```makefile
CXX = g++ ##制定编译器
TARGET =  hello 
OBJ = main.o printhello.o xxx.o

$(TARGET): $(OBJ)
	$(CXX) -O $(TARGET) $(OBJ)
	
main.o: main.cpp
	$(CXX) -C main.cpp
	
printhello.o: printhell0.cpp
	$(CXX) -C printhello.cpp
```

 #只编译修改过的文件



#version3

```makefile
CXX = g++ ##制定编译器
TARGET =  hello 
OBJ = main.o printhello.o xxx.o

CXXFLAGS = -C -wall ##编译选项

$(TARGET): $(OBJ)
	$(CXX) -O $@ $^  ## @ =TARGET  ^=OBJ (所有的) < OBJ (第一个) 

%.o: %.cpp
	$(CXX) $(CXXFLAGS)$< -O $@

.PHONY: clean ## 防止clean已经生成
clean:
	rm -f *.o $(TARGET) #删除 .o 和 TARGET文件
```

#如果有新文件添加 直接在OBJ 里面添加就好

#version4

```makefile
CXX = g++ 
TARGET =  hello 
SRC =$(wildcard *.cpp) #当前目录所有cpp 放入src
OBJ = $(patsubst %.cpp,%.o,$(SRC)) #路径替换 把SRC中所有xx.cpp 改为xx.o

CXXFLAGS = -C -wall ##编译选项

$(TARGET): $(OBJ)
	$(CXX) -O $@ $^  ## @ =TARGET  ^=OBJ (所有的) < OBJ (第一个) 

%.o: %.cpp
	$(CXX) $(CXXFLAGS)$< -O $@

.PHONY: clean ## 防止clean已经生成
clean:
	rm -f *.o $(TARGET) #删除 .o 和 TARGET文件
```

#自动获取.cpp文件