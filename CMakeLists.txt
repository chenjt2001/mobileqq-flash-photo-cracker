cmake_minimum_required(VERSION 3.10)
project(mobileqq_fp_cracker C)

set(CMAKE_C_STANDARD 17)

# 设置通用编译器选项
set(common_compiler_args "-Wall")

# 针对不同平台设置编译器选项
if(MSVC)
    # MSVC编译器选项
    set(CMAKE_C_FLAGS_DEBUG "${common_compiler_args} /DEBUG /DDEBUG /WX /experimental:c11atomics")
    set(CMAKE_C_FLAGS_RELEASE "${common_compiler_args} /O2 /DNDEBUG /WX /experimental:c11atomics")
else()
    # GCC/Clang编译器选项
    set(CMAKE_C_FLAGS_DEBUG "${common_compiler_args} -g -ggdb -fsanitize=address -DDEBUG -Werror")
    set(CMAKE_C_FLAGS_RELEASE "${common_compiler_args} -O3 -DNDEBUG -Werror")
endif()

# 添加可执行文件
add_executable(fp_cracker main.c)

# 链接库
if(MSVC)
    target_link_libraries(fp_cracker tomcrypt)
else()
    target_link_libraries(fp_cracker libtomcrypt.a pthread)
endif()
