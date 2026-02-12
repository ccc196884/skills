---
name: c-cpp-testing
description: C/C++ test pitfalls — Google Test patterns, sanitizer usage, memory leak detection in tests. Load only when writing or reviewing test files.
---

# C/C++ Testing — What Claude Gets Wrong

## Framework Choice
- **Check CMakeLists.txt / Makefile first** — use whatever the project uses
- C++: Google Test (gtest) is most common. Catch2 is simpler alternative.
- C: Unity, CMocka, or project-specific framework
- Don't introduce a new framework without checking existing setup

## Google Test Patterns
```cpp
TEST(ParserTest, EmptyInputReturnsError) {
    auto result = Parse("");
    ASSERT_FALSE(result.ok());
    EXPECT_EQ(result.error(), ErrorCode::kEmptyInput);
}

TEST_F(DatabaseTest, InsertAndRetrieve) {
    // TEST_F for fixtures — shares SetUp/TearDown
    db_->Insert("key", "value");
    EXPECT_EQ(db_->Get("key"), "value");
}
```

## Critical Mistakes
- **`ASSERT_*` stops test, `EXPECT_*` continues** — use `ASSERT` for preconditions, `EXPECT` for verifications
- **Memory leaks in tests are still bugs** — run tests with AddressSanitizer
- Don't test private methods — test through public interface
- Fixtures (`TEST_F`): `SetUp()` and `TearDown()` are per-test, not per-suite

## Sanitizers in Tests
- Compile tests with: `-fsanitize=address,undefined -fno-omit-frame-pointer`
- ASan catches: use-after-free, buffer overflow, memory leaks
- UBSan catches: signed overflow, null deref, misaligned access
- **If tests pass without sanitizers but fail with them, you have a real bug**

## CMake Integration
```cmake
enable_testing()
add_executable(tests test_main.cpp test_parser.cpp)
target_link_libraries(tests GTest::gtest_main)
gtest_discover_tests(tests)
```
