---
layout: post
title: "Roman to Integer"
---

## Problem
Given a Roman numeral string `s`, convert it to an integer. Roman numerals are usually written largest to smallest from left to right, except for the subtractive cases (e.g., `IV = 4`, `IX = 9`, `XL = 40`, `XC = 90`, `CD = 400`, `CM = 900`).

Constraints: `1 <= s.length <= 15`, `s` contains only `I, V, X, L, C, D, M`.

## Approach
- Map each Roman character to its integer value.
- Scan left to right:
  - If the current value is less than the next value, subtract it.
  - Otherwise, add it.

This works because subtractive pairs are the only time a smaller numeral precedes a larger one.

## Complexity
- **Time**: O(n) where n is the length of `s`.
- **Space**: O(1) extra space.

## C++ Code
```cpp
#include <string>
using namespace std;

class Solution {
public:
    int romanToInt(const string& s) {
        static int values[256] = {0};
        static bool initialized = false;
        if (!initialized) {
            values['I'] = 1;
            values['V'] = 5;
            values['X'] = 10;
            values['L'] = 50;
            values['C'] = 100;
            values['D'] = 500;
            values['M'] = 1000;
            initialized = true;
        }

        int total = 0;
        for (size_t i = 0; i < s.size(); i++) {
            int val = values[(unsigned char)s[i]];
            int next = (i+1 < s.size()) ? values[(unsigned char)s[i+1]] : 0;
            total += (val < next) ? -val : val;
        }
        return total;
    }
};
