Using `int` and `char` is usually a beginner-friendly way of coding. However, in the future there will be a need to have more portability; a need to be able to run your code in as many architectures as possible. Therefore, using `int` and `char` may not stick.

For that, one can use the following:

### Integer Types and Their Fixed-Width Equivalents

| Fixed-Width Type | Common Equivalent Type | Description             | Bit Width | Signed/Unsigned |
| ---------------- | ---------------------- | ----------------------- | --------- | --------------- |
| `int8_t`         | `signed char`          | 8-bit signed integer    | 8 bits    | Signed          |
| `uint8_t`        | `unsigned char`        | 8-bit unsigned integer  | 8 bits    | Unsigned        |
| `int16_t`        | `short`                | 16-bit signed integer   | 16 bits   | Signed          |
| `uint16_t`       | `unsigned short`       | 16-bit unsigned integer | 16 bits   | Unsigned        |
| `int32_t`        | `int`                  | 32-bit signed integer   | 32 bits   | Signed          |
| `uint32_t`       | `unsigned int`         | 32-bit unsigned integer | 32 bits   | Unsigned        |
| `int64_t`        | `long long`            | 64-bit signed integer   | 64 bits   | Signed          |
| `uint64_t`       | `unsigned long long`   | 64-bit unsigned integer | 64 bits   | Unsigned        |

This list feats only integers because technically characters are integers. However, before even going through that, there actually are equivalents of characters for explicit declarations:

### Character Types and Their Fixed-Width Equivalents

|Character Type|Fixed-Width Equivalent|Description|Bit Width|Signed/Unsigned|
|---|---|---|---|---|
|`char`|`int8_t` or `uint8_t`|Basic character representation|8 bits|Signed/Unsigned|
|`wchar_t`|`int16_t` / `uint16_t` or `int32_t` / `uint32_t`|Wide character representation|16 or 32 bits|Signed/Unsigned|
|`char16_t`|`uint16_t`|UTF-16 character representation|16 bits|Unsigned|
|`char32_t`|`uint32_t`|UTF-32 character representation|32 bits|Unsigned|
### Explanation

1. **`char`**:
    
    - In most systems, `char` is an 8-bit data type, capable of storing ASCII values (0 to 127) and sometimes extended ASCII (0 to 255).
    - Whether `char` is signed or unsigned depends on the platform/compiler, but you can explicitly use `int8_t` (signed) or `uint8_t` (unsigned) as fixed-width equivalents.
2. **`wchar_t`**:
    
    - `wchar_t` is used to represent wide characters, which means it can hold larger character sets than `char` (e.g., Unicode characters).
    - The exact size of `wchar_t` depends on the platform. It's often 16 bits on Windows (UTF-16) and 32 bits on Linux/Unix (UTF-32).
3. **`char16_t`** and **`char32_t`**:
    
    - These are introduced in C++11 and represent UTF-16 and UTF-32 encoded characters, respectively.
    - They are consistently 16 bits (`char16_t`) and 32 bits (`char32_t`) across platforms, making them suitable for handling Unicode data.

### Examples

- If you want to use an 8-bit integer to represent a `char` explicitly, you could use `int8_t` or `uint8_t`.
- For UTF-16 data, `char16_t` will always be 16 bits, equivalent to `uint16_t`.
- For UTF-32 data, `char32_t` will always be 32 bits, equivalent to `uint32_t`.

If needed, there's a section on UTF in [[What is UTF?]]