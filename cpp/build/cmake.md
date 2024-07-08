### 基本用法

在不同的平台下 需要创建不同的Makefile(麻烦)

 

```cmake
cmake_minimum_required (VERSION 2.8) #cmake 版本要求
 
project (hello) #项目名称
 
add_executable(hello hello.cpp) #生成可执行文件hello ，依赖参数
```

mkdir build #  存放生成的临时文件

cd build 

cmake ..



```cmake
cmake_minimum_required (VERSION 2.8) 
 
project (hello)

aux_source_directory(. SRC_LISTS)

include_directories(./inc_dir)
 
add_executable(hello ${SRC_LISTS})
```

aux_source_directory(dir var) #把**dir**目录中的所有源文件都储存在**var**变量中

include_directories(./inc_dir) # 在./inc_dir 目录下寻找头文件

### 多头文件和多源文件分离

```cmake
cmake_minimum_required (VERSION 2.8) 
 
project (hello)

#分开获取多个目录下所有源文件
aux_source_directory(src_dir1 SRC_LISTS1)
aux_source_directory(src_dir2 SRC_LISTS2)
aux_source_directory(main_dir1 main_LISTS)
 #引入多个头文件目录
include_directories(./inc_dir1 ./inc_dir1 )
 
add_executable(hello ${SRC_LISTS1} ${SRC_LISTS2} ${mian_LISTS})
```

