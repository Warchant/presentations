# dependency injection

+++

dynamic polymorphism:

```C++
class A{
    // must have only pure virtual methods
};

class B{
    B(A* a): a_(a){}

    A* a_;
}

class ConcreteA: public A{}
class MockA: public A{}

B b(new MockA());
B c(new ConcreteA());
```

@[5-9](class, which depends on A)
@[1-3](A's interface)
@[11](real implementation of class A)
@[12](mock implementation of class A)
@[14-15](usage)

+++

static polymorphism:

```C++
class ConcreteA{};
class MockA{};

template <typename T>
class B{
    T a;
}

B<ConcreteA> b;
B<MockA>     c;
```


+++

*we do not use this currently, just example*

`boost::di`

```C++

struct interface {
  virtual ~iworld() noexcept = default;
  virtual int get() const = 0;
};

class implementation : public interface {
public:
  int get() const override { return 42; }
};

struct example {
  example(std::shared_ptr<interface> i) {
    assert(42 == i->get());
  }
};

int main() {
  const auto injector = di::make_injector(
    di::bind<interface>.to<implementation>()
  );

  injector.create<std::unique_ptr<example>>();
}
```

motivational example:
http://boost-experimental.github.io/di/index.html#do-i-need-a-di-frameworklibrary
