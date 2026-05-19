# Understanding Operators in Python

Examples

```
op=10
oz=40

>>> op=10
>>> oz=200
>>> oz>10
True
>>> oz<10
False
>>>
>>> k=10
>>> l=10
>>> k>=l
True
>>>

```

## 🔢 1. Arithmetic Operators

Used for basic math operations.

|Operator|Name|Example|Result|
|---|---|---|---|
|`+`|Addition|`5 + 3`|`8`|
|`-`|Subtraction|`5 - 3`|`2`|
|`*`|Multiplication|`5 * 3`|`15`|
|`/`|Division (float)|`7 / 2`|`3.5`|
|`//`|Floor Division|`7 // 2`|`3`|
|`%`|Modulus (remainder)|`7 % 2`|`1`|
|`**`|Exponentiation|`2 ** 3`|`8`|

---

## 🔄 2. Assignment Operators

Used to assign (and often modify) values to variables.

|Operator|Example|Equivalent To|
|---|---|---|
|`=`|`x = 5`|Assign 5 to x|
|`+=`|`x += 3`|`x = x + 3`|
|`-=`|`x -= 3`|`x = x - 3`|
|`*=`|`x *= 3`|`x = x * 3`|
|`/=`|`x /= 3`|`x = x / 3`|
|`//=`|`x //= 3`|`x = x // 3`|
|`%=`|`x %= 3`|`x = x % 3`|
|`**=`|`x **= 3`|`x = x ** 3`|
|`&=`|`x &= 3`|`x = x & 3`|
|`\|=`|`x \|= 3`|`x = x \| 3`|
|`^=`|`x ^= 3`|`x = x ^ 3`|
|`>>=`|`x >>= 3`|`x = x >> 3`|
|`<<=`|`x <<= 3`|`x = x << 3`|
|`:=`|`if (n := 10) > 5:`|**Walrus operator** (assign + return, Python 3.8+)|

---

## ⚖️ 3. Comparison (Relational) Operators

Return `True` or `False` based on a comparison.

|Operator|Name|Example|Result|
|---|---|---|---|
|`==`|Equal to|`5 == 5`|`True`|
|`!=`|Not equal to|`5 != 3`|`True`|
|`>`|Greater than|`5 > 3`|`True`|
|`<`|Less than|`5 < 3`|`False`|
|`>=`|Greater than or equal|`5 >= 5`|`True`|
|`<=`|Less than or equal|`3 <= 5`|`True`|

> 💡 **Tip:** Python supports **chained comparisons** like `1 < x < 10`, which is equivalent to `1 < x and x < 10`.

---

## 🧠 4. Logical Operators

Used to combine conditional statements.

|Operator|Description|Example|Result|
|---|---|---|---|
|`and`|True if **both** are true|`True and False`|`False`|
|`or`|True if **at least one** is true|`True or False`|`True`|
|`not`|Inverts the boolean|`not True`|`False`|

> These use **short-circuit evaluation**: `and` stops at the first falsy value, `or` stops at the first truthy value.

---

## 🪪 5. Identity Operators

Check whether two variables refer to the **same object in memory** (not just equal values).

|Operator|Description|Example|
|---|---|---|
|`is`|True if same object|`x is y`|
|`is not`|True if **not** same object|`x is not y`|

a = [1, 2, 3]

b = a

c = [1, 2, 3]

  

a is b      # True  (same object)

a is c      # False (equal values, different objects)

a == c      # True  (equal values)

---

## 📦 6. Membership Operators

Check whether a value exists **in** a sequence (list, tuple, string, dict, set, etc.).

|Operator|Description|Example|
|---|---|---|
|`in`|True if value is found|`"a" in "apple"` → `True`|
|`not in`|True if value is **not** found|`5 not in [1,2,3]` → `True`|

---

## ⚙️ 7. Bitwise Operators

Operate on integers at the **binary (bit) level**.

|Operator|Name|Example|Result|
|---|---|---|---|
|`&`|AND|`5 & 3`|`1` (0101 & 0011 = 0001)|
|`\|`|OR|`5 \| 3`|`7` (0101 \| 0011 = 0111)|
|`^`|XOR|`5 ^ 3`|`6` (0101 ^ 0011 = 0110)|
|`~`|NOT (bitwise invert)|`~5`|`-6`|
|`<<`|Left shift|`5 << 1`|`10`|
|`>>`|Right shift|`5 >> 1`|`2`|

> Useful in network engineering for things like **subnet mask calculations** and **ACL bitmasks**—something you may encounter in your Cisco/ISE work.

---

## 🌟 8. Special / Other Operators

- **Unpacking operator (`*` and `**`):** Used to unpack iterables and dictionaries.
    
    a, *b = [1, 2, 3, 4]   # a=1, b=[2,3,4]
    
    merged = {**dict1, **dict2}  # merge dictionaries
    
- **Ternary (conditional) operator:** result = "even" if x % 2 == 0 else "odd"
    
- **Matrix multiplication (`@`):** Used with libraries like NumPy. result = matrix_a @ matrix_b
    

---

## 📋 Operator Precedence (Highest → Lowest)

|Priority|Operators|
|---|---|
|1 (highest)|`()` — Parentheses|
|2|`**` — Exponentiation|
|3|`~`, `+x`, `-x` — Unary|
|4|`*`, `/`, `//`, `%`|
|5|`+`, `-`|
|6|`<<`, `>>`|
|7|`&`|
|8|`^`|
|9|`\|`|
|10|`==`, `!=`, `>`, `<`, `>=`, `<=`, `is`, `is not`, `in`, `not in`|
|11|`not`|
|12|`and`|
|13 (lowest)|`or`|

> **When in doubt, use parentheses** `()` to make your intent explicit and your code more readable.

---

If you'd like to dive deeper into any specific category, or want to see practical examples (e.g., using bitwise operators for network calculations), just let me know! Your org also has a LinkedIn Learning course called Python Practice: Operations that covers hands-on challenges with Python operations. [[Python Pra...Operations | Viva Learning]](https://learning.cloud.microsoft/detail/09d21139-9043-435d-9da8-3ffb8b851831?context=%7B%22subEntityId%22:%7B%22source%22:%22M365Search%22%7D%7D)

----

