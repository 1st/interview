# Interview Questions with Algorithmic Tasks

Use this chapter as a conversation prep guide for the algorithm portion of interviews. Keep actual coding drills, deep explanations, and implementations in the dedicated [Algorithms & Data Structures repository](https://github.com/1st/algorithms/).

## Cheat Sheet
- Start answers with complexity targets (`O(n log n)` etc.) and mention trade-offs quickly.
- Narrate problem-solving steps: clarify, plan, code, test, optimize.
- Keep a mental map of key data structures (arrays, hash maps, trees, graphs) and go-to patterns.
- State your assumptions aloud, align on input constraints, and flag potential trade-offs before coding.

## Quick Refresh
- Recall how to describe time and space complexity using Big O, and rehearse concise definitions for `O(1)`, `O(n log n)`, and `O(n^2)`.
- Be ready to narrate your problem-solving process: clarify requirements, outline approach, validate with examples, and discuss trade-offs.
- Keep a short list of go-to data structures (arrays, hash maps, stacks/queues, trees/graphs) and what problems they fit.

## Talking Points by Theme

### Complexity Fundamentals
- Explain why Big O focuses on growth trends rather than exact timings.
- Discuss common optimization levers: reducing nested loops, precomputing, leveraging caching.

### Array & String Patterns
- Outline approaches for sliding window, two pointers, and prefix sums.
- Share how you'd handle Unicode or streaming input when relevant.

### Hash Map & Set Usage
- Highlight collision handling (chaining vs open addressing) and typical interview traps (mutable keys, ordering).
- Describe scenarios where counting or deduplication via hash structures accelerates solutions.

### Tree & Graph Reasoning
- Summarize DFS vs BFS trade-offs for search and shortest paths.
- Mention how you keep traversal states (visited sets, recursion stack) and detect cycles.

### Dynamic Programming Narratives
- Present the “overlapping subproblems + optimal substructure” definition succinctly.
- Show you can move from recursion to tabulation and reason about memory trade-offs.

## Interview Framing Tips
- **Clarify first:** Restate the prompt, confirm input format, size limits, data ranges, and edge cases.
- **Outline aloud:** Share the approach before coding; compare brute force vs optimized strategies.
- **Sample walkthrough:** Run through a non-trivial example step by step. Use it to verify your algorithm and catch off-by-one errors.
- **Complexity statement:** Commit to time/space complexity up front and revisit after coding to confirm.
- **Coding style:** Use clean variable names, modular helper functions, and narrate what you’re typing.
- **Testing:** Execute your example plus edge cases (empty, singleton, extremes) verbally. Mention how you’d test in production.
- **Refinement:** Proactively discuss optimizations, trade-offs, or alternative data structures even if you shipped a working version.
- **Learning loop:** Tie the outcome back to prior practice — reference similar problems from the [Algorithms & Data Structures repository](https://github.com/1st/algorithms/).

## Deep Dive Later
- Schedule focused coding sessions in the Algorithms & Data Structures repo to reinforce techniques.
- Capture post-practice reflections there; keep this guide as your high-level conversation map.
- Study company-specific question patterns and align them to the themes above for targeted prep.
