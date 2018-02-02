# test frameworks

+++ 

in Iroha we use GTEST and GMOCK frameworks

https://github.com/google/googletest

+++

### typical test

+++

```C++

#include <gtest/gtest.h>

TEST(TestSetName, TestCaseName){
    ASSERT_TRUE(false) << "I appear " << "if assertion fails";
}

```

+++

```C++

#include <gtest/gtest.h>

class TestSetA: public ::testing::Test {
    TestSetA(){
        member_var = 1337;
    }

    void SetUp(){}

    void TearDown(){}

    int member_var;
};

TEST_F(TestSetA, TestCase){
    ASSERT_EQ(member_var, 1337) << "not equal :(";
}
```

+++

In CMake:

```CMake
# macro:
addtest(testname testfile.cpp)
target_link_libraries(testname
    A
    B
    C
    )
target_compile_definitions(testname PUBLIC
    -DDISABLE_COMPATIBILITY=1
    )
target_include_directories(testname PUBLIC
    /tmp/somelib/include
    )
```

+++

### typical mocking procedure

+++

mock header:

```C++
#include <gmock/gmock.h>
#include "storage.hpp"

class MockStorage : public Storage {
 public:
  MOCK_CONST_METHOD0(getWsvQuery, std::shared_ptr<WsvQuery>(void));
  MOCK_CONST_METHOD0(getBlockQuery, std::shared_ptr<BlockQuery>(void));
  MOCK_METHOD0(createTemporaryWsv, std::unique_ptr<TemporaryWsv>(void));
  MOCK_METHOD0(createMutableStorage, std::unique_ptr<MutableStorage>(void));
  MOCK_METHOD1(doCommit, void(MutableStorage *storage));
  MOCK_METHOD1(insertBlock, bool(model::Block block));
  MOCK_METHOD0(dropStorage, void(void));

  void commit(std::unique_ptr<MutableStorage> storage) override {
    doCommit(storage.get());
  }
};

```

+++

mock usage:

```
class FixtureTest...{
      storageMock = std::make_shared<MockStorage>();
...
};

TEST_F(FixtureTest, Storage) {
    EXPECT_CALL(*storageMock, getBlockQuery())
          .WillRepeatedly(Return(block_query));
}
```


+++

benchmark -- https://github.com/google/benchmark
