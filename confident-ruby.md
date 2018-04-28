## Confident Ruby

> by [Avdi Grimm](http://www.virtuouscode.com/)

If you like the notes, go ahead and [buy the book](https://pragprog.com/book/agcr/confident-ruby)!

- **write methods which tell a story**
- performing work
  - `"The foundation of an object oriented system is the message"`
  - trusting **method input**
    - messages we want to send
    - find corresponding "roles"
    - ensure method logic receives objects, which can play those "roles"
  - design a method
    - identify **messages** we want to send (use problem domain language)
    - determine the **roles**, which should receive those messages (without knowledge of current API / objects / tools)
      - `"This omission was intentional. When we set out to write a method with our minds filled with knowledge about existing objects and their capabilities, it often gets in the way of identifying the vital plot of the story we are trying to tell. Like a MacGuyver solution, the tale becomes more about the tools we happen to have lying around than about the mission we first set out to accomplish.."`
    - **bridge the gap** between **roles** we identified and **existing objects** in the system
    - if you don't think about this process:
      - roles which you identify might be the same as existing classes
      - messages language will be dictated by existing methods
      - in consequence abstraction level will vary in one method
    - guard the borders of your methods (public API, internal modules borders in large apps)
- **collecting input**
  - use built-in conversion protocols (`to_str` / `to_s`)
  - call conversion method conditionally (`filename = filename.to_path if filename.respond_to?(:to_path)`)
    - `"Inputs are checked, but in a way that is open for extension"`
  - define own conversion protocols if needed
  - use built-in conversion functions
    - std-lib : `URI()`, `Pathname()`
    - when calling `Integer(value)`, we are effectively saying “convert this to an Integer, if there is any sensible way of doing so”, `Integer('stupid") # => ArgumentError`
    - arrays - `Array(String|Array|nil|Hash|Range) # => [ .. ]`
  - replace "string typing" with classes
  - wrap collaborators in adapters (in constructor)
  - reject unworkable values with preconditions (in constructor)
    - one of the purposes of a constructor is to establish an object’s invariant: a set of properties which should always hold true for that object
  - use `#fetch` to assert the presence of Hash keys
  - handle special cases with a Guard Clause `return unless/if ...`
  - represent special cases as objects (`current_user` / `guest`)
  - represent do-nothing cases as null objects (`NullLogger`)
  - substitute a benign value for `nill`
  - use symbols as placeholders objects (`options.fetch(:credentials) { :credentials_not_set }`)
  - bundle arguments into parameter objects
-  ...
