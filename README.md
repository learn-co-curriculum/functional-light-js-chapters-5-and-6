# FP Light JS: Chapters 5 & 6

## Chapter 5

### What I Loved

- The readability of a side effection function is worse because it requires more reading to understand the program.
- Writing code with one or multiple side effects burdens the reader with having to metally execute your program in its entirery up to a certain line, for them to read and understand that line.
- Use fixed, non-reassigned references (variables/functions) inside of another function as they will not change throughout the program.
- His description of race conditions as a side effect.
- His examples for idempotent vs non-idempotent operations

  ```javascript
  obj.count = 2;
  a[a.length - 1] = 42;
  person.name = upper( person.name );

  // non-idempotent:
  obj.count++;
  a[a.length] = 42;
  person.lastUpdated = Date.now();

  // DOM updates
  var hist = document.getElementById( "orderHistory" );

  // idempotent:
  hist.innerHTML = order.historyText;

  // non-idempotent:
  var update = document.createTextNode( order.latestUpdate );
  hist.appendChild( update );
  ```

- His push to try to make idempotent code, but understanding that it might not always be possible.
- Using referential transparency for testing if a function is truly pure.
- Encapsulating performance effects, so that you always hear when a tree falls in the forest, even if your not around

  ```javascript
  var specialNumber = (function memoization(){
    var cache = [];

    return function specialNumber(n){
        // if we've already calculated this special number,
        // skip the work and just return it from the cache
        if (cache[n] !== undefined) {
            return cache[n];
        }

        var x = 1, y = 1;

        for (let i = 1; i <= n; i++) {
            x += i % 2;
            y += i % 3;
        }

        cache[n] = (x * y) / (n + 1);

        return cache[n];
    };
  })();
  ```

- Sensible approaches to refactoring code with side effects to not hide the side effect as much and make the side effect call a pure function.
  ```javascript
  function addMaxNum(arr) {
    var maxNum = Math.max( ...arr );
    return maxNum + 1;
  }

  var nums = [4,2,7,3];

  nums.push(
      addMaxNum( nums )
  );

  nums;       // [4,2,7,3,8]
  ```

### What I Hated and/or Confused me

- His code snippet for shared state with AJAX calls was overly complex (fetchuUserData, fetchOrders, deleteOrder)

### Question Block

1. Does anyone have an experience they remember where relying on a side effect caused a ton of headache when trying to find a bug?
2. Do we have a specific block of code in Ironboard that uses side effects we think we could eliminate?
3. What did you think about his process of describing "Purely Relative"?
4. How do we test for referential transparency to see if a function is pure?
5. How do we handle references set as a `const` variable type if the data type is an Object? (Object or Array)?
6. How can we use the concept of safer functions in Ironboard (or any code)?



## Chapter 6

### What I Loved

- Value immutability, the notion that in our programs we use only values that cannont be changed
- Is description of non-locals (non-primitive values become non-local)
- A constant is a variable that cannot be reassigned.
- Use libraries for immutably setting arrays
- If your not sure if an arg/passed reference is immutable make it immutable in the function.

### What I Hated and/or Confused me

- Why not rely on the possiblity that the `const` key word might cause some potential bugs in your code or bad refactors instead of using only `let`? I know it wont stop all value mutation, but it gives you some error messages which are better than none.
- Focusing too much on his coding styles views versus do they make sense or follow FP principles.

### Question Block

1. Should we only use `const` for numbers, floats, booleans, & strings?


<p class='util--hide'>View <a href='https://learn.co/lessons/functional-light-js-chapters-5-and-6'>Functional Light JS Chapters 5 and 6</a> on Learn.co and start learning to code for free.</p>
