### 编写 C++ 代码
```cpp
// example.cpp
extern "C" {
    int add(int a, int b) {
        return a + b;
    }
}
```

### 使用 g++ 编译为共享库
linux
```
g++ -shared -fPIC -o libexample.so example.cpp
```

macOS
```
g++ -dynamiclib -o libexample.dylib example.cpp
```

解释：
-shared：指示编译器生成共享库。  
-fPIC：生成位置无关的代码（Position Independent Code），适合共享库。  
-o libexample.so：指定输出文件名为 libexample.so（Linux）或 libexample.dylib（macOS）。

### 运行 Python 代码调用共享库

import ctypes

```python
# 加载共享库
lib = ctypes.CDLL('./libexample.so')  # 对于 Linux
# lib = ctypes.CDLL('./libexample.dylib')  # 对于 macOS

# 调用 add 函数
result = lib.add(3, 5)
print(result)  # 输出 8
```
