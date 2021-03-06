## Jest: Expect & Matchers

### Most Common Matchers

`toEqual(val)`:
  : Most common equality matcher. Compares objects or arrays by comparing contents, not identity.

`toMatch(/hello/)`:
  : Tests against regular expressions or strings.


### Expecting an Error

`toThrow(message)`:
  : Tests the function will throw an error.

~~~ {.javascript}
describe('#findById', () => {
  it('should throw if not a number', () => {
    expect(() => findById('invalid'))
      .toThrow('Must provide a number')
  })
})
~~~

### Expecting the Opposite

You can chain `not` to test the opposite

~~~ {.javascript}
it('test the opposite', () => {
  expect(0).not.toEqual(1)
})
~~~

### Other Matchers Sometimes Used

`toContainEqual(x)`:
  : Expect an array to contain `x`.

`toBe(x)`:
  : Compares with `x` using `===`.

`toBeTruthy()`:
  : Should be true `true` when cast to a Boolean.

`toBeFalsy()`:
  : Should be `false` when cast to a Boolean.

`arrayContaining(array)`:
  : Checks it's a subset (order doesn't matter).

### Exercise: Writing a Test with Jest

  #. Open `src/www/js/jest/__tests__/adder.spec.js`

  #. Do exercise 1

  #. To test and debug, run

~~~
cd src
yarn test www/js/jest/__tests__/adder.spec.js
~~~
