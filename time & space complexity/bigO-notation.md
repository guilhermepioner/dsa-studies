# :books: Summary

1. [What is Big O Notation](#timer_clock-what-is-big-o-notation)
    - [O(n) function](#on-function)
    - [About scaling time](#warning-about-scaling-time)
    - [Constants](#constants)
    - [Growth Hierarchy](#growth-hierarchy)
0. [References](#references)

# :timer_clock: What is Big O Notation?

Big O notation is a mathematical model that help us identify, classify and analyze algorithms by their efficiency and how they scales as its input approaches infinity

It indicates as the size of the input of the algorithm grows, how drastically do the space or time requirements grow with it

Big O notation is often represented by the letter O followed by paranthesis: _O()_

It can also be represented by the Greek letter Omega instead of O: _Ω()_

## O(n) function

```js
function linearFunc(arr) {
    for (let i=0; i<arr.length; i++) {
        console.log(1000 * 100000)  // It will always takes the same amount of time to execute => It's a constant time
    }
}

const arr = [1,2,3,4,5,6,7]
linearFunc(arr)
```

## :warning: About scaling time

**When considering the efficiency of a function, lines that take constat time DO NOT MATTER**

This is because if our array were some big length (e.g. 2kk) changing the constant expression to someting simpler would have a negligible effect on the efficiency of the function as a whole

Independent of how many constant expressions, we'd still say that the function **scales linearly** or is **O(n)**

This is a important point to note down. **Big O notation doesn't quantify how much time it will take to the algorithm execute, rather it classifies how it scales according to the input**

## Constants

**A constant is any step that doesn't scale with the input to the function**

For example:

```js
function constants(arr) {
    var result = 100 * 1000 // both 100 & 1000 are constants. These values are always the same
    return result;
}
```

The function above is known as _O(1)_ because the only operation within the function is constant which means it doesn't scale with any input

**Constant functions are always defined as Big O of 1 or _Ω(1)_**

## Growth Hierarchy

In Big O, we a wave a growth hierarchy, which looks something like this:

**📈 Orders of Growth:**

| Notation | Name  | Perfomance |
|-------|-------|-------|
| O(1)  | Constant | Best |
| O(_log_ n) | Logarithmic |
| O(n) | Linear |
| O(n _log_ n) | Linearithmic |
| O(n²) | Quadratic |
| O(n³) | Cubic |
| O(2^n) | Exponential |
| O(n!) | Factorial | Worst |

In Big O notation, when determining the efficiency of an algorithm, we only care about the worst case

**That's why constants are ignored, because we're only eliminating the non dominant items**

This is supported by the fact that as input moves towards infinity, constants become less and less significant

# References

- [Big O Notation - Full Course](https://www.youtube.com/watch?v=Mo4vesaut8g)
