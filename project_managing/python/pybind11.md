## code
### mathlib.hpp
```cpp
#pragma once

namespace mathlib {
    int add(int a, int b);
    double multiply(double a, double b);
    class Calculator {
    public:
        Calculator();
        double square(double x);
        double power(double base, int exponent);
    };
}
```

### mathlib.cpp
```cpp
#include "mathlib.hpp"

namespace mathlib {
    int add(int a, int b) {
        return a + b;
    }

    double multiply(double a, double b) {
        return a * b;
    }

    Calculator::Calculator() {}

    double Calculator::square(double x) {
        return x * x;
    }

    double Calculator::power(double base, int exponent) {
        double result = 1.0;
        for(int i = 0; i < exponent; ++i) {
            result *= base;
        }
        return result;
    }
}
```

### pybind11 wrapper: mathlib_wrapper.cpp
```cpp
#include <pybind11/pybind11.h>
#include "mathlib.hpp"

namespace py = pybind11;

PYBIND11_MODULE(mathlib_python, m) {
    m.doc() = "Python bindings for mathlib"; // Optional module docstring
    
    m.def("add", &mathlib::add, "Add two integers");
    m.def("multiply", &mathlib::multiply, "Multiply two doubles");
    
    py::class_<mathlib::Calculator>(m, "Calculator")
        .def(py::init<>())
        .def("square", &mathlib::Calculator::square)
        .def("power", &mathlib::Calculator::power);
}
```

### setup.py
```python
from setuptools import setup, Extension
import pybind11

mathlib_module = Extension('mathlib_python',
                            sources=['mathlib.cpp', 'mathlib_wrapper.cpp'],
                            include_dirs=[pybind11.get_include()],  # Add this line
                            extra_compile_args=['-std=c++11'])  # or '-std=c++17'

setup(name='mathlib_python',
      version='1.0',
      ext_modules=[mathlib_module])
```

### example_usage.py
```python
import mathlib_python

def test_mathlib():
    # Test basic functions
    result1 = mathlib_python.add(5, 3)
    print(f"5 + 3 = {result1}")
    
    result2 = mathlib_python.multiply(4.5, 2.0)
    print(f"4.5 * 2.0 = {result2}")
    
    # Test Calculator class
    calc = mathlib_python.Calculator()
    result3 = calc.square(3.0)
    print(f"3.0² = {result3}")
    
    result4 = calc.power(2.0, 3)
    print(f"2.0³ = {result4}")

if __name__ == "__main__":
    test_mathlib()
```

## 编译和安装：
```bash
python setup.py install
```
