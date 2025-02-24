I want you to act as a software developer
Generate the Unit Tests using the new Swift Testing framework

Here is changes from XCTests:

''' swift

Convert test classes
// Before
class FoodTruckTests: XCTestCase {
...
}

// After
struct FoodTruckTests {
...
}

Convert test methods
// Before
class FoodTruckTests: XCTestCase {
func testEngineWorks() { ... }
...
}

// After
struct FoodTruckTests {
@Test func engineWorks() { ... }
...
}
'''

Here is a matrix of changes for the XCT macros in the new Swift Testing framework:

| XCTest | SwiftTesting |
|--------|--------------|
| XCTAssert(x) | #expect(x) |
| XCTAssertTrue(x) | #expect(x) |
| XCTAssertFalse(x) | #expect(!x) |
| XCTAssertNil(x) | #expect(x == nil) |
| XCTAssertNotNil(x) | #expect(x != nil) |
| XCTAssertEqual(x, y) | #expect(x == y) |
| XCTAssertNotEqual(x, y) | #expect(x != y) |
| XCTAssertIdentical(x, y) | #expect(x === y) |
| XCTAssertNotIdentical(x, y) | #expect(x !== y) |
| XCTAssertGreaterThan(x, y) | #expect(x > y) |
| XCTAssertGreaterThanOrEqual(x, y) | #expect(x >= y) |
| XCTAssertLessThanOrEqual(x, y) | #expect(x <= y) |
| XCTAssertLessThan(x, y) | #expect(x < y) |
| XCTAssertThrowsError(try f()) | #expect(throws: (any Error).self) { try f() } |
| XCTAssertThrowsError(try f()) { error in … } | let error = #expect(throws: (any Error).self) { try f() } |
| XCTAssertNoThrow(try f()) | #expect(throws: Never.self) { try f() } |
| try XCTUnwrap(x) | try #require(x) |
| XCTFail("…") | Issue.record("…") |

Always use #expect for all assertions in the generated tests



Your additional guidelines:

Generated Test class should be marked as @MainAction

Design Small, Focused Tests: Each unit test should focus on one functionality, enhancing readability and ease of debugging. Ensure each test is isolated and does not depend on others. Simulate the behavior of external dependencies using mock objects to increase the reliability and speed of your tests.

Tests should follow a clear structure and use descriptive names to make their purpose clear. 

Provide detailed descriptions and comments for Tests and their asserts

Implement the AAA Pattern: Implement the Arrange-Act-Assert (AAA) paradigm in each test, establishing necessary preconditions and inputs (Arrange), executing the object or method under test (Act), and asserting the results against the expected outcomes (Assert).
