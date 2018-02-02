# terms

+++

**unit test**

The purpose of a unit test is to verify the behavior of a relatively small piece of software, independently from other parts. Unit tests are narrow in scope, and allow us to cover all cases, ensuring that every single part works correctly.

+++

**unit test**

![](https://i.imgur.com/6gxwNz9.png)

+++

**integration test**

On the other hand, integration tests demonstrate that different parts of a system work together in the real-life environment. They validate complex scenarios (we can think of integration tests as a user performing some high-level operation within our system), and usually require external resources, like databases or web servers, to be present.

+++

**integration test**

![](https://i.imgur.com/Akys1PO.png)

+++

**regression test**

Refers to the practice of comparing the results of running a program given a specific input with a fixed set of expected results, in order to verify that the program continues to behave as expected from one version to the next.

+++

**regression test**

```C++
const auto TESTCASE = {
    {"a", 5},
    {"a", 6},
    {"b", 1}
};

const auto EXPECTED = {
    {"a", 6},
    {"b", 1}
};

TEST(Map, SameKeyInsert){
    auto db = map();
    for(const auto& c: TESTCASE){
        auto [key, val] = c;
        db->insert(key, val);
    }
    for(const auto& e: EXPECTED){
        auto actual = db->find(e.first());
        auto expected = e.second();
        ASSERT_EQ(actual, expected);
    }
}
```

+++

**system test**

System testing of software or hardware is testing conducted on a complete, integrated system to evaluate the system's compliance with its specified requirements.
System testing falls within the scope of black-box testing, and as such, should require no knowledge of the inner design of the code or logic.

+++

*white-box testing*

Refers to the practice of verifying the expected behavior of a component by exploiting knowledge of its underlying implementation.

*black-box testing*

Refers to the practice of verifying the expected behavior of a component based solely on its specification (without knowledge of its implementation).
