# gmockglobal
This header-only library implements gmock functionality for global functions. Like for the class methods in original gmock you wrote ```MOCK_METHOD#N``` for mocking some method, you can now write ```MOCK_GLOBAL_FUNC#N``` and mock some function from global scope. 

# USING
Syntaxis is most similar to gmock. For example, to mock function ```multiply``` with two ```double``` arguments and ```double``` result you have to write declaration: 
```
MOCK_GLOBAL_FUNC2(multiply, double(double, double));
```

You can check call count of such function using ```EXPECT_GLOBAL_CALL``` macro, same as you used ```EXPECT_CALL``` macro for classes: 
```
EXPECT_GLOBAL_CALL(multiply, multiply(1, 2));
```

The ```.Times(...)``` and other methods will be work too. 

# SAMPLES
For the samples see [repo](https://github.com/apriorit/gmockglobal_sample)