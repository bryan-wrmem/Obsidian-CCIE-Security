# Understanding Loops in Python

Loop - repetition

Two main types

For and While loops

While - runs until condition is true
For - run for each x in y






-----

# 🔁 Python Loops — A Beginner's Guide

Loops let your program **repeat things automatically**. Instead of writing the same code over and over, you tell Python: _"Keep doing this until I say stop."_

---

## 🧠 The Core Idea

Imagine you need to greet 5 people. Without loops:

print("Hello, Alice!")

print("Hello, Bob!")

print("Hello, Charlie!")

print("Hello, Dana!")

print("Hello, Eve!")

With a loop:

names = ["Alice", "Bob", "Charlie", "Dana", "Eve"]

  

for name in names:

    print(f"Hello, {name}!")

Same result, but **cleaner, shorter, and scalable** — even if the list had 5,000 names.

---

## 🔹 1. The `for` Loop — "Do this for each item"

The `for` loop is the **most common loop** in Python. It walks through a sequence (list, string, range, etc.) **one item at a time**.

### ✅ Syntax

for item in sequence:

    # do something with item

### ✅ Looping through a list

fruits = ["apple", "banana", "cherry"]

  

for fruit in fruits:

    print(fruit)

**Output:**

```
apple
banana
cherry
```

### ✅ Looping through a string (character by character)

for letter in "Python":

    print(letter)

**Output:**

```
P
y
t
h
o
n
```

> 🔑 **Key concept:** The variable name after `for` (like `fruit` or `letter`) is your choice — pick something **descriptive** that makes your code readable.

---

## 🔹 2. The `range()` Function — "Loop a specific number of times"

When you want to repeat something a **set number of times**, use `range()`.

### ✅ Basic: `range(stop)`

Counts from `0` up to (but **not including**) the stop number.

for i in range(5):

    print(i)

**Output:**

```
0
1
2
3
4
```

> ⚠️ **Beginner trap:** `range(5)` gives you 5 numbers, but starts at `0` and ends at `4`, not `5`.

### ✅ With a start: `range(start, stop)`

for i in range(1, 6):

    print(i)

**Output:** `1 2 3 4 5`

### ✅ With a step: `range(start, stop, step)`

for i in range(0, 10, 2):

    print(i)

**Output:** `0 2 4 6 8`

### ✅ Counting backwards

for i in range(5, 0, -1):

    print(i)

**Output:** `5 4 3 2 1`

### 📋 Quick `range()` Reference

|Expression|Produces|
|---|---|
|`range(5)`|`0, 1, 2, 3, 4`|
|`range(1, 6)`|`1, 2, 3, 4, 5`|
|`range(0, 10, 2)`|`0, 2, 4, 6, 8`|
|`range(10, 0, -1)`|`10, 9, 8, ... 1`|
|`range(5, 5)`|_(empty — nothing runs)_|

---

## 🔹 3. The `while` Loop — "Keep going while this is true"

A `while` loop repeats **as long as a condition stays true**. You don't need to know in advance how many times it will run.

### ✅ Syntax

while condition:

    # do something

### ✅ Example: Counting up

count = 1

  

while count <= 5:

    print(count)

    count += 1       # Don't forget this!

**Output:** `1 2 3 4 5`

### ✅ Example: User input loop

password = ""

  

while password != "secret":

    password = input("Enter password: ")

  

print("Access granted!")

This keeps asking **until** the user types `"secret"`.

> ⚠️ **DANGER — Infinite loops!** If the condition **never becomes false**, your loop runs forever:
> 
> # ❌ This will never stop!
> 
> while True:
> 
>     print("Help!")
> 
> Always make sure something inside the loop **changes the condition** so it can eventually end. If you accidentally create one, press `Ctrl + C` to stop it.

---

## 🔹 4. `for` vs `while` — When to use which?

|Situation|Use|
|---|---|
|You know **how many times** to loop|`for`|
|You're going through a **list/sequence**|`for`|
|You **don't know** how many times — depends on a condition|`while`|
|Waiting for **user input** or an **event**|`while`|

> 💡 **Rule of thumb:** If you can use a `for` loop, prefer it. It's harder to accidentally create an infinite loop with `for`.

---

## 🔹 5. Loop Control Statements

These keywords give you **extra control** over how a loop behaves.

### 🛑 `break` — "Stop the loop immediately"

Exits the loop entirely, even if there are more items or the condition is still true.

for number in range(1, 10):

    if number == 5:

        print("Found 5! Stopping.")

        break

    print(number)

**Output:**

```
1
2
3
4
Found 5! Stopping.
```

### ⏭️ `continue` — "Skip this one, move to the next"

Skips the **rest of the current iteration** and jumps to the next one.

for number in range(1, 6):

    if number == 3:

        continue          # Skip 3

    print(number)

**Output:**

```
1
2
4
5
```

### 💤 `pass` — "Do nothing (placeholder)"

Does absolutely nothing. Useful when you need a block of code **syntactically** but aren't ready to write it yet.

for number in range(5):

    pass    # TODO: add logic later

### Quick Comparison

|Keyword|What it does|
|---|---|
|`break`|**Exits** the entire loop|
|`continue`|**Skips** the current iteration|
|`pass`|**Does nothing** (placeholder)|

---

## 🔹 6. The `else` Clause on Loops

This surprises many beginners — Python loops can have an `else` block! It runs **only if the loop completed normally** (wasn't stopped by `break`).

### ✅ Example: Search pattern

numbers = [1, 3, 7, 9, 11]

  

for num in numbers:

    if num % 2 == 0:

        print(f"Found an even number: {num}")

        break

else:

    print("No even numbers found.")

**Output:** `No even numbers found.`

> Read it like: _"**For** each number, check if it's even. If you finish the loop without breaking, **else** tell me none were found."_

---

## 🔹 7. Nested Loops — "A loop inside a loop"

You can put one loop **inside** another. The inner loop runs **completely** for each pass of the outer loop.

for row in range(1, 4):

    for col in range(1, 4):

        print(f"({row},{col})", end="  ")

    print()   # New line after each row

**Output:**

```
(1,1)  (1,2)  (1,3)
(2,1)  (2,2)  (2,3)
(3,1)  (3,2)  (3,3)
```

### ✅ Practical example: Multiplication table

for i in range(1, 6):

    for j in range(1, 6):

        print(f"{i * j:4}", end="")

    print()

**Output:**

```
   1   2   3   4   5
   2   4   6   8  10
   3   6   9  12  15
   4   8  12  16  20
   5  10  15  20  25
```

> 💡 **Tip:** Nested loops multiply iterations. A loop of 100 × a loop of 100 = **10,000 iterations**. Be mindful of performance.

---

## 🔹 8. Helpful Loop Techniques

### `enumerate()` — Get the index AND the value

colors = ["red", "green", "blue"]

  

for index, color in enumerate(colors):

    print(f"{index}: {color}")

**Output:**

```
0: red
1: green
2: blue
```

> Way cleaner than manually tracking a counter variable!

### `zip()` — Loop through two lists at once

names = ["Alice", "Bob", "Charlie"]

scores = [90, 85, 78]

  

for name, score in zip(names, scores):

    print(f"{name}: {score}")

**Output:**

```
Alice: 90
Bob: 85
Charlie: 78
```

### `reversed()` — Loop backwards

for i in reversed(range(1, 4)):

    print(i)

**Output:** `3 2 1`

### 📋 Quick Reference

|Technique|What it does|
|---|---|
|`enumerate(seq)`|Gives you **(index, value)** pairs|
|`zip(a, b)`|Pairs items from **two sequences** together|
|`reversed(seq)`|Iterates in **reverse order**|
|`sorted(seq)`|Iterates in **sorted order**|

---

## ⚠️ Common Beginner Mistakes

### 1. Forgetting to update the `while` condition

# ❌ Infinite loop — count never changes

count = 0

while count < 5:

    print(count)

  

# ✅ Fixed

count = 0

while count < 5:

    print(count)

    count += 1

### 2. Modifying a list while looping through it

# ❌ Unexpected behavior

numbers = [1, 2, 3, 4, 5]

for num in numbers:

    if num % 2 == 0:

        numbers.remove(num)

  

# ✅ Loop over a copy instead

for num in numbers[:]:     # [:] creates a copy

    if num % 2 == 0:

        numbers.remove(num)

### 3. Off-by-one errors with `range()`

# ❌ Prints 0-4 (not 1-5)

for i in range(5):

    print(i)

  

# ✅ Prints 1-5

for i in range(1, 6):

    print(i)

### 4. Using `==` instead of `in` for membership

# ❌ Only checks one value

if color == "red" or "blue":   # Always True! (bug)

  

# ✅ Correct

if color in ["red", "blue"]:

---

## 🎯 Practice Challenges

Build your confidence with these:

1. **Easy:** Print every number from 1 to 20.
2. **Easy:** Loop through a list of your favorite foods and print each one.
3. **Medium:** Print only the **even numbers** from 1 to 50.
4. **Medium:** Use a `while` loop to keep asking the user to guess a number until they get it right.
5. **Stretch:** Print a right triangle of stars:
    
    ```
    *
    **
    ***
    ****
    *****
    ```
    
6. **Stretch:** Use `enumerate()` to print a numbered shopping list from a Python list.

---

## 🗺️ Where You've Been & Where You're Going

|✅ Covered|📍 You Are Here|⬜ Up Next|
|---|---|---|
|Operators|**Loops**|Functions|
|Conditionals||Data Structures (lists, dicts)|

Loops + conditionals together are the **backbone of all programming logic**. Once you're comfortable combining them, you can build just about anything.

---

Want me to continue the series with **functions** or **data structures** next? Or if you'd like, I can put together a hands-on mini-project that ties operators, conditionals, and loops all together 🚀