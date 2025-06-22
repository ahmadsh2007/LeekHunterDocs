# Response Schema Specification - Alpha Version of LeekHunter

This document defines the expected JSON output format from the Gemini API for code analysis.

---

## 🎯 Required Fields (Per Bug Object)

- **bug_description** (string):  
  A concise explanation of the bug.

- **fix_suggestion** (string):  
  A suggested fix for the **bugged line only**.

- **line_number** (integer):  
  The line where the bug occurs.

- **severity_level** (string):  
  One of: `"Low"`, `"Minor"`, `"Major"`, `"Critical"`.

---

## 📌 Example Output

```json
[
  {
    "bug_description": "The `while` loop in `processQueue` is an infinite loop because the processed item is accessed using `queue[0]` but is never removed from the queue. This prevents the `queue.length` from ever decreasing to zero, causing the loop condition to always remain true and leading to an unresponsive application.",
    "fix_suggestion": "Change `const item = queue[0];` to `const item = queue.shift();` to correctly remove the processed item from the front of the queue in each iteration.",
    "line_number": 25,
    "severity_level": "Critical"
  },
  {
    "bug_description": "The function continuously adds new items to the queue using `queue.push(newItem);` for every item processed. This design, especially when combined with the lack of item removal, leads to indefinite queue growth and potential memory exhaustion. If the intention is to process a finite set of items or to eventually empty the queue, this continuous addition is a logical flaw.",
    "fix_suggestion": "Re-evaluate the logic for adding new items. If the queue is meant to eventually empty or process a finite set of tasks, this line `queue.push(newItem);` should be removed or made conditional based on specific termination criteria.",
    "line_number": 30,
    "severity_level": "Major"
  }
]
