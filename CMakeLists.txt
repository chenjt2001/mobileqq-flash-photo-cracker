cmake_minimum_required(VERSION 3.10)
project(mobileqq_fp_cracker C)

set(CMAKE_C_STANDARD 11)

# 设置通用编译器选项
set(common_compiler_args "-Wall -Werror -Wno-unused")

# 针对不同平台设置编译器选项
if(MSVC)
    # MSVC编译器选项
    set(CMAKE_C_FLAGS_DEBUG "${common_compiler_args} /DEBUG /DDEBUG")
    set(CMAKE_C_FLAGS_RELEASE "${common_compiler_args} /O2 /DNDEBUG")
else()
    # GCC/Clang编译器选项
    set(CMAKE_C_FLAGS_DEBUG "${common_compiler_args} -g -ggdb -fsanitize=address -DDEBUG")
    set(CMAKE_C_FLAGS_RELEASE "${common_compiler_args} -O3 -DNDEBUG")
endif()

# 添加可执行文件
add_executable(fp_cracker main.c)

# 链接库
if(MSVC)
    target_link_libraries(fp_cracker tomcrypt)
else()
    target_link_libraries(fp_cracker libtomcrypt.a pthread)
endif()
