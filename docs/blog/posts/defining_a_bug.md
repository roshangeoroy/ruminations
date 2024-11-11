---
date: 2024-11-11
authors: [roshan]
description: >
    Silly bug I encountered recently
categories:
  - Blog

---

# Always Use Braces with Your `#define` Expressions!

Recently, I discovered the actual working of `#define`. When you use `#define` for expressions, it doesn’t evaluate or compile the expression at that point; it simply copies the expression wherever it appears in the code during the pre-processing stage.
<!-- more -->
Check out the example below to see why this can be an issue:

```c
#define ONE_BYTE 1
#define TYPE ONE_BYTE
#define ID ONE_BYTE
#define HEADER_LENGTH TYPE + ID

uint8_t calcPayloadLength(uint8_t total_length) {
    uint8_t payload_length = total_length - HEADER_LENGTH;
    return payload_length;
}
```

If you didn’t catch it, here’s what happens: since the value is copied directly, `HEADER_LENGTH` will be replaced by `1 + 1`. The expression becomes `total_length - 1 + 1`, which is not what we expected. Wrapping the `#define` expression in parentheses would fix this.

For some reason, I assumed that, because I was defining constants, the compiler would optimize it and replace `HEADER_LENGTH` with `2` instead of `1 + 1`. I tried different optimization levels and realized that optimization doesn’t affect the pre-processing stage.

I have to admit, it took me about an hour to pinpoint this bug in my code! The issue surfaced only after I switched from hard-coded numbers to macros, as my linter suggested.

So, always remember: **use braces with `#define` expressions!**
