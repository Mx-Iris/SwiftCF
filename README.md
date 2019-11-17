# SwiftCF

[![Github CI Status](https://github.com/ddddxxx/SwiftCF/workflows/CI/badge.svg)](https://github.com/ddddxxx/SwiftCF/actions)

Using CoreFoundation in Swift painlessly.

## Usage

### Dynamic casting to CoreFoundation types via the type-id mechanism.

```
import SwiftCF

let str: Any = "foo" as CFString

let s0 = str as? CFString
// ❗️ Conditional downcast to CoreFoundation type 'CFString' will always succeed

let s1: CFString = cfCast(str) // or
let s2 = cfCast(str, to: CFString.self) // or
let s3 = CFString.cast(str)
// ✅
```

### Toll-Free-Bridging

```
let cfStr: CFString = .from("foo")
let nsStr: NSString = cfStr.asNS
let str: NSString = cfStr.asSwift
```

### Convenient Extensions

```
let str = "foo" as CFString

str.length
// Replace CFStringGetLength(str)

CFStringTokenizer.create(string: str)
// Replace 😱 CFStringTokenizerCreate(kCFAllocatorDefault, str, CFRange(location: 0, length: CFStringGetLength(str)), kCFStringTokenizerUnitWord, CFLocaleGetSystem())
```

### Swift Protocol Conformance

```
let arr = [1, 3.14, "foo"] as CFArray

for item in arr {
    // 😃 CFArray now conforms to RandomAccessCollection.
}
```

## Requirements

- Swift 5.0+
