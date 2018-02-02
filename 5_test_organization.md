# test organization

+++

project structure

```
.
├── iroha-cli
├── irohad
├── libs
├── schema
├── shared_model
└── test
```

+++

test structure

```
test
├── benchmark
├── framework
├── integration
│   ├── consensus
│   └── pipeline
└── module
    ├── irohad
    │   ├── ametsuchi
    │   ├── api
    │   ├── common
    │   ├── consensus
    │   ├── logger
    │   ├── model
    │   ├── network
    │   ├── ordering
    │   ├── simulator
    │   ├── synchronizer
    │   ├── torii
    │   └── validation
    ├── libs
    │   ├── amount
    │   ├── cache
    │   ├── common
    │   ├── converter
    │   ├── crypto
    │   ├── datetime
    │   └── validator
    ├── shared_model
    │   ├── backend_proto
    │   ├── bindings
    │   ├── cryptography
    │   ├── lazy_test.cpp
    │   └── validators
    └── vendor
```
