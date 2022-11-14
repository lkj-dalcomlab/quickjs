## quickjs project cmake include
### sample
``` cmake
FetchContent_Declare(  
    qjs  
    GIT_REPOSITORY https://github.com/lkj-dalcomlab/quickjs.git  
    GIT_TAG v0.5  
)  
FetchContent_MakeAvailable(qjs)
add_execute(test main.cpp)
target_link_libraries(test PRIVATE qjs-core)
```