## Software Design X-Rays: Fix Technical Debt with Behavioral Code Analysis 

> Adam Tornhill

If you like the notes, go ahead and [buy the book](https://www.goodreads.com/book/show/36517037-software-design-x-rays)!

- What do we want to achieve?
  - Find **Hot-Spots** - places in the code with high "interest rate",
  - Hot-Spots are code fragments worth improving - fixing them means saved development time in the future
  - the goal is to prioritize technical debt
- How to find Hot-Spots?
  - By Change Frequency (number of changes over time)
    - code changed too often signals possible problems with design
  - By Complexity (number of LoC, indentations)
    - too large modules are hard/impossible to reason about (regardless of its change frequency)
  - Combining above metrics, visualize it
  - Apply Organization/Team/Project context

- Hot Spot
  - has low cohesion - contains several unrelated parts, lacks modularity

- Change Coupling
  - files (lines, components) which are changed within the same commit

Interesting insights
 - Tests complexity - use test setup heuristic
 - Modules complexity - number of indentations heuristic
