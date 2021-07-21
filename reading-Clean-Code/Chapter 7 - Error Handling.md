# Error Handling

by Michael Feathers

## Use Exceptions Rather Than return Codes

## Write Your Try-Catch-Finally Statement First

- Exceptions _define a scope_ within your program.
- The `catch` has to leave the program in a consistent state.

## Use Unchecked Exceptions

- Checked Exceptions violate the Open/Closed principle
  - Checked exceptions force you to declare that exception in the signature of each method between you and the catch
- Checked Exceptions break encapsulation

## Provide Context with Exceptions

- Create informative error messages and pass them along with your exceptions

## Define Exception Classes in Terms of a Caller's Needs

- How they are caught

## Define the Normal Flow

- Avoid using try/catch statements for unique exceptions from usual logic.
- Create a class or configure an object to handle the special case

## Don't Return Null

- _Really calling me out here..._
- Null checks have become normalized
- NULL CHECKS SHOULD NOT BE NORMAL
- This is why strict typing of languages is extremely important.
- This is why _typescript_ is extremely important
- If some sort of get method that usually returns an array can be expected to be null when the result is going to be looped, why not just send an empty array? This is a simple example, but this thought process is important to apply in all situations.

## Don't Pass Null

- Just don't.

<br/>
<br/>

# Conclusion

Clean code is readable, but it must also be robust. These are not conflicting goals. We can
write robust clean code if we see error handling as a separate concern, something that is
viewable independently of our main logic. To the degree that we are able to do that, we can
reason about it independently, and we can make great strides in the maintainability of our
code.
