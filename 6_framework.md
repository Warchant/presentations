# iroha testing framework

+++

### test_subscriber

```
test/framework/test_subscriber.hpp
```

+++

```C++
make_test_subscriber<VerificationStrategy>()

VerificationStrategy {
  CallExact,   // checks invariant that subscriber is called exact number of times
  IsCompleted  // Checks that on_completed is called by observable
}


+++

```C++
TEST_F(BlockQueryTest, GetBlocksFrom0) {
  auto wrapper =
      make_test_subscriber<CallExact>(blocks->getBlocksFrom(AmetsuchiTest::FIRST_BLOCK), blocks_total);
  size_t counter = AmetsuchiTest::FIRST_BLOCK;
  wrapper.subscribe([&counter](Block b) {
    // wrapper returns blocks 1 and 2
    ASSERT_EQ(b.height, counter++) << "block height: " << b.height
                                   << "counter: " << counter;
  });
  ASSERT_TRUE(wrapper.validate());
}
```

+++

### test_block_generator

```
test/framework/test_block_generator.{c,h}pp
```

+++

```C++

iroha::model::Transaction getAddPeerTransaction(uint64_t create_time,
                                                std::string address);

iroha::model::Transaction getTestCreateTransaction(uint64_t create_time);

iroha::model::Block generateBlock();
```

