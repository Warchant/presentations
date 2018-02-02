# some rules

+++

**always inject dependencies using static/dynamic polymorphism** or with use of special libs such as `boost::di`. 

it allows you to replace class dependencies in tests with mocks -- in fact, this allows you to write unit tests for class with dependencies.

+++

**make your tests as linear as possible** -- if test has branch conditions like this:

```C++
auto a = testable_method();
if(a < 10){
	ASSERT_EQ(a, 5);
} else {
	ASSERT_EQ(a, 15);
}
```

then it is bad test! it can be separated on two independent tests.

every test case should test single execution path.

+++

**follow project test structure**

+++

**always test interface (do black-box testing), not implementation.**

tests which exploit implementation details (white-box tests) must be separated from the rest.

+++

**never write "private" free functions, which are inside cpp files.**

if method exists but not accessible from outside, it means that it is not possible to write a test for this method.

better make a separate utils class/package, which will provide these methods for your cpp implementation.

+++

**test all public API of your component.**

+++

**use test coverage metrics** to write quality tests. 

https://docs.codecov.io/docs/about-code-coverage

