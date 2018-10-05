# gmock-global [![Build Status](https://travis-ci.org/apriorit/gmock-global-sample.svg?branch=master)](https://travis-ci.org/apriorit/gmock-global-sample)
This header-only library implements [gmock](https://github.com/google/googletest/blob/master/googlemock) functionality for global functions. 

- [Introduction](#introduction)
- [Usage](#usage)
  - [Step 1: Adding includes](#step-1-adding-includes)
  - [Step 2: Declare mock global](#step-2-declare-mock-global)
- [Known issues](#known-issues)
- [Samples](#samples)
- [License](#license)
- [Version history](#version-history)
  - [Version 1.0.0 (17 Oct 2017)](#version-100-17-oct-2017)
  
# Introduction
[Gmock](https://github.com/google/googletest/blob/master/googlemock) is a C++ framework for writing [mock classes](https://en.wikipedia.org/wiki/Mock_object). It is very convenient to create mock objects for mocking of methods. But [gmock](https://github.com/google/googletest/blob/master/googlemock) can not mock global functions. This problem is quite common but has no trivial solution. [Gmock FAQ](https://github.com/google/googlemock/blob/master/googlemock/docs/FrequentlyAskedQuestions.md#my-code-calls-a-staticglobal-function--can-i-mock-it) says you are doing something wrong if you need to mock static or global functions. However it is required in some cases and [gmock-global](https://github.com/apriorit/gmock-global) provides such functionality.

# Usage

## Step 1: Adding includes
At first your project needs to know about [gmock-global](https://github.com/apriorit/gmock-global).
1. Add `gmock-global/include` to the project include paths.
2. Add `#include <gmock-global/gmock-global.h>` after [gmock](https://github.com/google/googletest/blob/master/googlemock) include.

## Step 2: Declare mock global
Syntax is most similar to [gmock](https://github.com/google/googletest/blob/master/googlemock). For example, to mock function `multiply` with two `double` arguments and `double` result you have to write declaration: 
```cpp
MOCK_GLOBAL_FUNC2(multiply, double(double, double));
```
You can check call count of such function using `EXPECT_GLOBAL_CALL` macro, same as you used `EXPECT_CALL` macro for classes: 
```cpp
EXPECT_GLOBAL_CALL(multiply, multiply(1, 2));
```

The `.Times(...)` and other methods will be work too. 

In result mocking of global `double multiply(double, double)` looks like:
```cpp
MOCK_GLOBAL_FUNC2(multiply, double(double, double));

...

TEST(TestGlobal, CanMultiplyGlobal)
{
    EXPECT_GLOBAL_CALL(multiply, multiply(1, 2)).Times(1);
    multiply(1, 2);
}
```

[gmock-global](https://github.com/apriorit/gmock-global) supports more than 10 arguments. It requires [gmock-more-args](https://github.com/apriorit/gmock-more-args) in such case. 


# Known issues
The [after clause](https://github.com/google/googletest/blob/master/googlemock/docs/CheatSheet.md#the-after-clause) can't be using with [gmock-global](https://github.com/apriorit/gmock-global), use `Sequences` instead.

# Samples
Samples live in the separate [repository](https://github.com/apriorit/gmock-global-sample)

# License
[gmock-global](https://github.com/apriorit/gmock-global) is licensed under the MIT License. You can freely use it in your commercial or opensource software.

# Version history

## Version 1.0.0 (17 Oct 2017)
- Initial public release
