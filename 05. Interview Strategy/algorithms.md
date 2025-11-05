# Interview Questions with Algorithmic Tasks

Use this chapter as a conversation prep guide for the algorithm portion of interviews. Keep actual coding drills, deep explanations, and implementations in the dedicated [Algorithms & Data Structures repository](https://github.com/1st/algorithms/). Treat this page as the five-minute reset before a loop or the night-before cram.

**Prep Snapshot:** confirm the interview format, pick one representative pattern to rehearse, note what signal you want to emphasize (communication, trade-offs, testing), and queue up a single follow-up drill in the external repo for later.

## Quick Practice Loop
- Pick one medium-level problem aligned with the upcoming role; spend 5 minutes clarifying constraints before touching the keyboard.
- Pseudocode aloud, then solve in your preferred language; timebox to 20 minutes and narrate checkpoints the way you would with the interviewer.
- Debrief immediately: compare with an editorial/solution, capture new patterns in spaced notes, and flag any follow-up questions.
- Log or tag the session in the external repo so you can trend common gaps and queue the next drill.

## Cheat Sheet
- Start answers with complexity targets (`O(n log n)` etc.) and mention trade-offs quickly.
- Narrate problem-solving steps: clarify, plan, code, test, optimize.
- Keep a mental map of key data structures (arrays, hash maps, trees, graphs) and go-to patterns.
- State your assumptions aloud, align on input constraints, and flag potential trade-offs before coding.

## Rapid Memory Joggers
- Recall quick definitions for time and space complexity (especially `O(1)`, `O(n log n)`, `O(n^2)`) and how you justify them aloud.
- Rehearse the narrative arc: clarify, plan, code, test, optimize — mention this structure explicitly at the start of the interview.
- Keep a short list of go-to data structures (arrays, hash maps, stacks/queues, trees/graphs) and the interview prompts where you would reach for each.

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
- **Outline aloud:** Share the approach before coding; compare brute force vs optimized strategies and explain the trade-off decision.
- **Sample walkthrough:** Run through a non-trivial example step by step. Use it to verify your algorithm and catch off-by-one errors.
- **Complexity statement:** Commit to time/space complexity up front and revisit after coding to confirm.
- **Coding style:** Use clean variable names, modular helper functions, and narrate what you’re typing.
- **Testing:** Execute your example plus edge cases (empty, singleton, extremes) verbally. Mention how you’d test in production.
- **Refinement:** Proactively discuss optimizations, trade-offs, or alternative data structures even if you shipped a working version.
- **Learning loop:** Tie the outcome back to prior practice — reference similar problems from the [Algorithms & Data Structures repository](https://github.com/1st/algorithms/) and queue deeper drills there instead of here.

## Deep Dive Later
- Pair each practice session with at least one write-up in your personal notes or the external repo; explain the pattern as if teaching it.
- Schedule focused coding sessions in the Algorithms & Data Structures repo to reinforce techniques.
- Capture post-practice reflections there; keep this guide as your high-level conversation map.
- Study company-specific question patterns and align them to the themes above for targeted prep.
