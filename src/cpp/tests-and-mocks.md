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

Mocks are used for testing the behaviour of APIs or interfaces which will be used in the component under test. A _mock object_ implements the same interface as a real object but you can specity at run time how it will be used and what it should do (which methods will be called? in which order? how many times? with what arguments? what will they return?).

### Basics

Google Mock involes three basic steps:
1. Use some simple macros to describe the interface you want to mock, and they will expand to the implementation of your mock class
2. Create some mock objects and specify its expectation and behaviour using an intuitive syntax
3. Exercise code that uses the mock objects. Google Mock will catch any violation of the expectations as soon as it arises



At the top of your file `#include <gmock/gmock.h>`










