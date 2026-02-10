# Swift Testing (XCTest)

## Defaults

- Use XCTest
- Prefer protocol-based mocks
- Use async tests when needed

## Minimal examples

## Example

```swift
import XCTest
@testable import MyApp

final class NormalizeDateTests: XCTestCase {
    func testReturnsIsoDate() throws {
        let iso = try normalizeDate("2026-01-31", timeZone: "UTC")
        XCTAssertEqual(iso, "2026-01-31")
    }
}
```
