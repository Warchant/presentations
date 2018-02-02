# testable code

+++

![](http://image.slidesharecdn.com/mockobject-110410235909-phpapp02/95/mock-object-14-728.jpg?cb=1302480140)

+++

interface: 
```
ametsuchi/peer_query.hpp
```

```C++
class PeerQuery {
 public:
  virtual nonstd::optional<std::vector<model::Peer>> getLedgerPeers() = 0;

  virtual ~PeerQuery() = default;
};
```

+++

implementation:
```
ametsuchi/impl/peer_query_wsv.{h,c}pp
```

```C++
class PeerQueryWsv : public PeerQuery {
 public:
  explicit PeerQueryWsv(std::shared_ptr<WsvQuery> wsv);

  nonstd::optional<std::vector<model::Peer>> getLedgerPeers() override;

 private:
  std::shared_ptr<WsvQuery> wsv_;
};
```

+++

mock implementation:
```
test/module/irohad/ametsuchi/ametsuchi_mocks.hpp
```


```C++
class MockPeerQuery : public PeerQuery {
 public:
  MockPeerQuery() = default;

  MOCK_METHOD0(getLedgerPeers,
               nonstd::optional<std::vector<model::Peer>>());
};
```

+++

test code:

```C++
TEST_F(BlockLoaderTest, ValidWhenSameTopBlock) {
  // Current block height 1 => Other block height 1 => no blocks received
  Block block;
  block.height = 1;

  EXPECT_CALL(*peer_query, getLedgerPeers()).WillOnce(Return(peers));
  EXPECT_CALL(*storage, getTopBlocks(1))
      .WillOnce(Return(rxcpp::observable<>::just(block)));
  EXPECT_CALL(*storage, getBlocksFrom(block.height + 1))
      .WillOnce(Return(rxcpp::observable<>::empty<Block>()));
  auto wrapper =
      make_test_subscriber<CallExact>(loader->retrieveBlocks(peer.pubkey), 0);
  wrapper.subscribe();

  ASSERT_TRUE(wrapper.validate());
}
```

@[6](during test, we expect getLedgerPeers() in mock to be called once and return `peers` array.)

