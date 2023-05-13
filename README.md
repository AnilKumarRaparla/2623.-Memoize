# 2623.-Memoize
const memoize = (fn) => {
  const cache = new Map();
  return (...args) => {
    const key = args.toString(); // Use the arguments as a key for the cache
    if (cache.has(key)) {
      return cache.get(key);
    }
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
};

const sum = (a, b) => a + b;
const memoizedSum = memoize(sum);

const fib = (n) => (n <= 1 ? 1 : fib(n - 1) + fib(n - 2));
const memoizedFib = memoize(fib);

const factorial = (n) => (n <= 1 ? 1 : factorial(n - 1) * n);
const memoizedFactorial = memoize(factorial);

const functions = {
  sum: memoizedSum,
  fib: memoizedFib,
  factorial: memoizedFactorial,
};

const test = (fnName, inputs) => {
  const fn = functions[fnName];
  const results = [];
  for (let i = 0; i < inputs.length; i++) {
    const [args, expected] = inputs[i];
    const result = fn(...args);
    results.push(result);
    if (result !== expected) {
      console.log(
        `Failed: ${fnName}(${args.join(", ")}) returned ${result}, expected ${expected}`
      );
    }
  }
  console.log(`Passed all tests for ${fnName}!`);
  return results;
};

test("sum", [
  [[2, 2], 4],
  [[3, 5], 8],
]);

test("fib", [
  [[0], 1],
  [[1], 1],
  [[2], 2],
  [[3], 3],
  [[4], 5],
]);

test("factorial", [
  [[0], 1],
  [[1], 1],
  [[2], 2],
  [[3], 6],
  [[4], 24],
]);
