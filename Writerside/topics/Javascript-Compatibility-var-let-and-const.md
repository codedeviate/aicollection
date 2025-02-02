# var, let and const

When it comes to backwards compatibility for variable declarations (`var`, `let`, and `const`) in browsers, here's a detailed breakdown of their support across different versions:

## 1. `var`
- **Introduced in**: ECMAScript 5 (ES5) — 2009
- **Compatibility**: `var` has been supported since very early versions of JavaScript, and **all browsers** support it, including **Internet Explorer** (IE 6+).

- **Behavior**:
    - **Global scope**: Variables declared with `var` are scoped to the function (or globally if declared outside a function).
    - **Hoisting**: Variables declared with `var` are hoisted to the top of their scope, meaning they can be accessed before their declaration (though their value will be `undefined` until the declaration line is reached).

## 2. `let`
- **Introduced in**: ECMAScript 6 (ES6) — 2015
- **Compatibility**:
    - Supported in **modern browsers** like Chrome, Firefox, Edge, Safari, and Opera (since 2015, around version 49+ in Chrome).
    - **Not supported in**: Internet Explorer (IE 11 and earlier).

- **Behavior**:
    - **Block-scoped**: Variables declared with `let` are scoped to the nearest enclosing block (e.g., inside loops or conditionals).
    - **No hoisting**: While `let` is hoisted, it is not initialized until the line of declaration. If accessed before the declaration, it results in a **ReferenceError** (often referred to as the "temporal dead zone").

## 3. `const`
- **Introduced in**: ECMAScript 6 (ES6) — 2015
- **Compatibility**:
    - Supported in **modern browsers** like Chrome, Firefox, Edge, Safari, and Opera (since 2015, around version 49+ in Chrome).
    - **Not supported in**: Internet Explorer (IE 11 and earlier).

- **Behavior**:
    - **Block-scoped**: Like `let`, `const` is scoped to the nearest block.
    - **Immutability**: Variables declared with `const` cannot be reassigned after initialization. However, the contents of objects and arrays (declared with `const`) are **mutable**.
    - **No hoisting**: Similar to `let`, `const` is hoisted but in a "temporal dead zone," so trying to access it before declaration results in a **ReferenceError**.

## Summary of Compatibility:
| Feature     | IE 6-8 | IE 9-10 | IE 11 | Chrome (from) | Firefox (from) | Safari (from) | Edge (from) | Opera (from) |
|-------------|--------|---------|-------|---------------|----------------|---------------|-------------|--------------|
| **`var`**   | Yes    | Yes     | Yes   | Yes (All)     | Yes (All)      | Yes (All)     | Yes (All)   | Yes (All)    |
| **`let`**   | No     | No      | No    | Yes (49)      | Yes (54)       | Yes (10)      | Yes (12)    | Yes (36)     |
| **`const`** | No     | No      | No    | Yes (49)      | Yes (54)       | Yes (10)      | Yes (12)    | Yes (36)     |

### Key:
- **IE 6-8**: Internet Explorer versions 6 to 8.
- **IE 9-10**: Internet Explorer versions 9 and 10.
- **IE 11**: Internet Explorer version 11.
- **Chrome (from)**: The first Chrome version that supports the feature.
- **Firefox (from)**: The first Firefox version that supports the feature.
- **Safari (from)**: The first Safari version that supports the feature.
- **Edge (from)**: The first Edge version that supports the feature.
- **Opera (from)**: The first Opera version that supports the feature.

## Conclusion:
- `var` is supported in **all browsers**, even older versions like Internet Explorer 6+.
- `let` and `const` are **not supported in Internet Explorer** (any version) and are supported in **modern browsers** (Chrome, Firefox, Safari, Edge, Opera) from 2015 onwards.
- If you need to support older browsers like IE, it’s safer to stick with `var`. For modern development, using `let` and `const` is recommended due to their block-scoping and immutability benefits.