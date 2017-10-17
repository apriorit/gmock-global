# gmock-global
This header-only library implements [gmock](https://github.com/google/googletest/blob/master/googlemock) functionality for global functions. 

# Introduction
[Gmock](https://github.com/google/googletest/blob/master/googlemock) is a C++ framework for writing [mock classes](https://en.wikipedia.org/wiki/Mock_object). It is very convenient to create mock objects for mocking of methods. But if we want to mock global function there are no any support from [gmock](https://github.com/google/googletest/blob/master/googlemock). This problem is quite common but have no trivial solution. [Gmock FAQ](https://github.com/google/googlemock/blob/master/googlemock/docs/FrequentlyAskedQuestions.md#my-code-calls-a-staticglobal-function--can-i-mock-it) says you are doing wrong if yo need to mock static or global function.\
Like for the class methods in original gmock you wrote `MOCK_METHOD#N` for mocking some method, you can now write `MOCK_GLOBAL_FUNC#N` and mock some function from global scope. 

# Usage

## Step 1: Adding includes
At first your project needs to know about [gmock-global](https://github.com/apriorit/gmock-global).
1. Add `gmock-global/include` to the project include paths.
2. Add `#include <gmock-global/gmock-global.h>` after [gmock](https://github.com/google/googletest/blob/master/googlemock) include.

## Step 2: Declare mock global
Syntax is most similar to gmock. For example, to mock function ```multiply``` with two ```double``` arguments and ```double``` result you have to write declaration: 
```
MOCK_GLOBAL_FUNC2(multiply, double(double, double));
```

You can check call count of such function using ```EXPECT_GLOBAL_CALL``` macro, same as you used ```EXPECT_CALL``` macro for classes: 
```
EXPECT_GLOBAL_CALL(multiply, multiply(1, 2));
```

The ```.Times(...)``` and other methods will be work too. 

# Samples
For the samples see [repo](https://github.com/apriorit/gmock-global_sample)

# License
[gmock-global](https://github.com/apriorit/gmock-global) is licensed under the MIT License. You can freely use it in your commercial or opensource software.

# Version history

## Version 1.0.0 (17 Oct 2017)
- Initial public release