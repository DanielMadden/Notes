# Use Intention-Revealing Names

- If a name requires a comment, then the name does not reveal its intent

```c#
int d; // elapsed time in days
```

```c#
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

```c#
public List<int[]> getThem() {
    List<int[]> list1 = new ArrayList<int[]>();
    for (int[] x : theList)
        if (x[0] == 4)
            list1.add(x);
    return list1;
}
```

- Why is it hard to tell what this code is doing?

  - No complex expressions
  - Spacing and indentation are reasonable
  - Only three variables
  - Only two constants

- The problem isn't the simplicity of the code
- The problem is the _implicity_ of the code
  - the degree to which the context is not explicit in the code itself.
- The code implicitly requires that we know the answers to questions such as:
  1. What kinds of things are in `theList`?
  2. What is the significance of the zeroth subscript of an item in `theList`?
  3. What is the significance of the value `4`?
  4. How would I use the list being returned?

# Avoid Disinformation

- Avoid words with entrenched meanings
- Do not refer to a grouping of accounts as an `accountList` unless it's actually a `List`. Any of these would work better:
  - `accountGroup`
  - `bunchOfAccounts`
  - `accounts`

# Make Meaningful Distinctions

# Use Pronounceable Names

# Use Searchable Names

# Avoid Encodings

# Avoid Mental Mapping

# Class Names: `Nouns`

- Classes and objects should have noun or noun phrase names like
  - `Customer`
  - `WikiPage`
  - `Account`
  - `AddressParser`
- Avoid words like `Manager`, `Processor`, `Data`, or `Info` in the name of a class. A class name should not be a verb.

# Method Names: `Verbs`

- Methods should have verb or verb phrase names like
  - `postPayment`
  - `deletePage`
  - `save`

# Don't Be Cute

- Le `HolyHandGrenade`

# Pick One Word per Concept

# Don't Pun

# Use Solution Domain Names

# Use Problem Domain Names

# Add Meaningful Context

# Don't Add Gratuitous Context

# Final Words
