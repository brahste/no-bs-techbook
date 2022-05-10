# Tests and Mocks with Google Test and Google Mock (incomplete)

__Links__

- https://stackoverflow.com/questions/13513905/how-to-set-up-googletest-as-a-shared-library-on-linux
- https://chromium.googlesource.com/external/github.com/google/googletest/+/refs/tags/release-1.8.0/googlemock/docs/ForDummies.md

## Google Test

### Basics

First, install `gtest` and `gmock` on your system from https://github.com/google/googletest. Follow the links above for information on how to do this.

At the top of your test file `#include <gtest/gtest.h>`

The main function (entry point) of all test scripts uses the following format
```c++
int main(int argc, char **argv) {
    testing::InitGoogleTest(&argc, argv);
    return RUN_ALL_TESTS();
}
```

Write your tests inside the scoped block.
```c++
TEST(TestName, subtest_name) {
    ...
}
```

__Note__: Stylistically it's best to divide your tests into seperate test files. In this case make sure that if your project build knows where to look for your test files. For example, if you use CMake then the test executable (set with `add_executable(...)`) needs to include the source test files and any required header files.

### Assertions

Assertions are used to validate the expected result the funcionality under test. Outcomes of assertions fall into 3 categories:
- Success
- Non-fatal failure
- Fatal failure

The outcome of the assertion depends on one of two assertion prefixes:
`ASSERT` assertions lead to fatal failures that halt the execution of the test
`EXPECT` assertions lead to non-fatal failure that allow the execution of the test to continue

A few important assertions are:
- `ASSERT_EQ()` / `EXPECT_EQ()` (or `_NE()` for not equal)
- `ASSERT_STREQ()` / `EXPECT_STREQ()` (or `_STRNE()` for not equal)
- `ASSERT_FALSE()` / `EXPECT_FALSE()` (or `_TRUE()`)
- `ASSERT_LT()` / `EXPECT_LT()` (or `_LE()` for less than or equal)
- `ASSERT_GT()` / `EXPECT_GT()` (or `_GE()` for greather than or equal)

__Note__: It is good practice to use only one assertion per test case.

### Writing Tests

Every unit test consists of three components:
- Arrange: Gather everything required to run the test
- Act: Run the test
- Assert: Verify the results of the test with an assertion

__Note__: Unit tests are self-contained, they should not require inputs or depend on the output of any other code.

### Test Fixtures

Test fixtures are standardized tests components that can be reused across different unit tests. To use test fixtures create a `struct` and add member functions `void SetUp()` and `void TearDown()`.

```c++
struct NameOfTestFixture : public testing::Test {
    NameOfTestClass tc;
    void SetUp() { tc = TestClass(1000); }
    void TearDown() { delete tc; }
};
```

Then pass the test fixture as the first parameter of the `TEST_F` that uses the fixture.

```c++
TEST_F(NameOfTestFixture, SubtestName) {
    ...
}
```

Using this approach the `NameOfTestClass` class will be available inside the `TEST_F` block (e.g. the tests that use the fixture). This can also be done with functions or variables as opposed to classes.
This allows you to consolidate the _arrange_ component of the unit tests since `SetUp()` and `TearDown()` will be called automatically when the `TEST_F` is executed.
Other standardized methods of the test fixture are also available. For example, `static void SetUpTestSuite()` and `static void TearDownTestSuite()` will run only once before the fixture's subtests are run as opposed to `SetUp()` and `TearDown()` which will run at before and after each `TEST_F` block.

## Google Mock
> Links:
> - http://google.github.io/googletest/gmock_for_dummies.html

Mocks are used for testing the behaviour of APIs or interfaces which will be used in the component under test. A _mock object_ implements the same interface as a real object but you can specity at run time how it will be used and what it should do (which methods will be called? in which order? how many times? with what arguments? what will they return?).

### Basics
At the top of your file `#include <gmock/gmock.h>`

Google Mock involes three basic steps:
1. Use some simple macros to describe the interface you want to mock, and they will expand to the implementation of your mock class
2. Create some mock objects and specify its expectation and behaviour
3. Exercise code that uses the mock objects. Google Mock will catch any violation of the expectations as soon as it arises

Use cases for gMock
- You are stuck with a sub-optimal design and wish you had done more prototyping before it was too late, but prototyping in C++ is by no means “rapid”.
- Your tests are slow as they depend on too many libraries or use expensive resources (e.g. a database).
- Your tests are brittle as some resources they use are unreliable (e.g. the network).
- You want to test how your code handles a failure (e.g. a file checksum error), but it’s not easy to cause one.
- You need to make sure that your module interacts with other modules in the right way, but it’s hard to observe the interaction; therefore you resort to observing the side effects at the end of the action, but it’s awkward at best.
- You want to “mock out” your dependencies, except that they don’t have mock implementations yet; and, frankly, you aren’t thrilled by some of those hand-written mocks.

Use gMock as:
- a *design* tool for experimenting with designs early and often
- a *testing* tool to cut test-time dependencies and validate interaction between modules.

Write a mock class by inheriting from the class you intend to mock and use the `MOCK_METHOD` macro.

#### Mock Notes
- mocks are objectspre-programmed with expectations, forming a specification of the calls ther are expected to receive
- mocking a proven and accepted practice inmany programming languages
- Steve added mocks to the *test/mocks/* directory.
- **Important note:** gMock requires expectations to be set **before** the mock functions are called, otherwise the behavior is **undefined**. Do not alternate between calls to `EXPECT_CALL()` and calls to the mock functions, and do not set any expectations on a mock after passing the mock to an API.
- Note that mocks don't have implementations, instead they shadow the implementation that you give them by specifying what they will return and how they will act.
- You should run tests on virtual base classes, since the mocks themselves don't have any implementation, this is the best way to mock the functionality.
- Careful to not use unprotected commas in your custom mocks
- All MOCK_METHODS must be publicly accessible
- If you don’t mock all versions of the overloaded method, the compiler will give you a warning about some methods in the base class being hidden. To fix that, use `using` to bring them in scope
- While it is advisable to mock virtual methods. It is also possible to mock non-virtual methods.

### Setting Expectations
The key to being good with mocks is to set the correct expectations on them.

### Types of Mocks
When a mock method is called but isn't set with expectations using `EXPECT_CALL()` an "uninteresting call" is made as specified by its `ON_CALL()` specification. By default, when a uninteresting call is made, a warning is emitted.
- To ignore these warning, wrap your mock object in a `NiceMock<T>` class.
- To make these warnings failures, wrap your mock object in a `StrictMock<T>` class.
- By default, your mocks are wrapped in a `NaggyMock<T>` class, which is why a warning is emitted when an uninteresting call is made.

Recommendation is that one should use `NaggyMock` for designing and debugging tests, `NiceMock` most of the time, and `StrictMock` only when it is absolutely required.

#### Mocking Functions
see https://github.com/google/googletest/blob/d9c55a48eddbc92434454ac2b28771870750e616/googlemock/docs/cook_book.md#mock-stdfunction-mockfunction

Use `MockFunction` which has a `Call(...args)` and `asStdFunction()`








