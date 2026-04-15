# Karpathy Guidelines Examples

Real-world anti-patterns and corrected approaches aligned with the original Karpathy-inspired doctrine.

---

## 1) Think Before Coding

### Example A: Hidden assumptions

User request: "Add a feature to export user data."

**Bad pattern (silent assumptions):**

- Assumes export scope is "all users"
- Assumes output format and destination
- Assumes which fields are safe to export
- Starts coding immediately

**Good pattern (surface assumptions first):**

```text
Before implementing, please confirm:
1) Scope: all users or filtered subset?
2) Delivery mode: API response, downloadable file, or background job?
3) Fields: which user fields are allowed to export?
4) Scale: expected record volume?

Simplest default is paginated JSON via API endpoint. Confirm?
```

### Example B: Multiple interpretations

User request: "Make search faster."

**Bad pattern:**

- Implements caching, async, and indexing all at once
- No confirmation about which "faster" matters

**Good pattern:**

```text
"Faster" can mean:
1) Lower latency per request
2) Higher throughput under concurrency
3) Better perceived UX responsiveness

Current baseline: ~500ms typical query.
Which target do you want first?
```

---

## 2) Simplicity First

### Example A: Over-abstraction

User request: "Add a function to calculate discount."

**Bad pattern:**

- Adds strategy classes, enums, config models
- Produces dozens of lines for a simple formula

**Good pattern:**

```python
def calculate_discount(amount: float, percent: float) -> float:
    return amount * (percent / 100)
```

Guideline:

- Add complexity only when requirements actually require multiple discount modes.

### Example B: Speculative features

User request: "Save user preferences to database."

**Bad pattern:**

- Adds cache abstraction, validation modes, merge flags, notification hooks
- Implements features never requested

**Good pattern:**

```python
def save_preferences(db, user_id: int, preferences: dict):
    db.execute(
        "UPDATE users SET preferences = ? WHERE id = ?",
        (json.dumps(preferences), user_id)
    )
```

Guideline:

- Add cache/validation/merge only if needed by explicit requirement or observed issue.

---

## 3) Surgical Changes

### Example A: Drive-by refactor during bug fix

User request: "Fix crash when email is empty."

**Bad pattern:**

- Rewrites validation architecture
- Changes comments, formatting, and unrelated username rules
- Modifies behavior beyond the requested bug

**Good pattern:**

```diff
 def validate_user(user_data):
-    if not user_data.get('email'):
+    email = user_data.get('email', '')
+    if not email or not email.strip():
         raise ValueError("Email required")
-    if '@' not in user_data['email']:
+    if '@' not in email:
         raise ValueError("Invalid email")
```

Guideline:

- Only the lines needed to fix empty-email handling are changed.

### Example B: Style drift

User request: "Add logging to upload function."

**Bad pattern:**

- Also adds type hints, rewrites quote style, changes return structure
- Reformats unrelated blocks

**Good pattern:**

```diff
+ import logging
+ logger = logging.getLogger(__name__)

  def upload_file(file_path, destination):
+     logger.info(f'Starting upload: {file_path}')
      try:
          ...
      except Exception as e:
-         print(f"Error: {e}")
+         logger.exception(f'Upload error: {file_path}')
          return False
```

Guideline:

- Match existing style and only add the requested capability.

---

## 4) Goal-Driven Execution

### Example A: Vague fix request

User request: "Fix authentication."

**Bad pattern:**

- Starts broad changes without defining success
- Ends with "should be fixed"

**Good pattern:**

```text
Define issue first (example: old sessions remain valid after password change).

Plan:
1) Write failing test that reproduces issue
   verify: test fails consistently
2) Implement session invalidation on password change
   verify: failing test now passes
3) Add edge-case tests (multi-session/concurrency)
   verify: edge tests pass
4) Run existing auth suite
   verify: no regressions
```

### Example B: Incremental rollout

User request: "Add rate limiting."

**Bad pattern:**

- Ships Redis + middleware + config system in one large change
- No staged verification

**Good pattern:**

```text
Step 1: in-memory limiter on one endpoint
verify: threshold test returns 429 after limit

Step 2: middleware for all endpoints
verify: existing endpoint tests still pass

Step 3: Redis backend for multi-instance
verify: counter shared across instances

Step 4: endpoint-specific configuration
verify: per-endpoint limits respected
```

### Example C: Reproduce before fix

User request: "Sorting fails when duplicate scores exist."

**Bad pattern:**

- Changes sort code without reproducing bug

**Good pattern:**

```python
def test_sort_with_duplicate_scores():
    scores = [
        {"name": "Alice", "score": 100},
        {"name": "Bob", "score": 100},
        {"name": "Charlie", "score": 90},
    ]
    result = sort_scores(scores)
    assert result[0]["score"] == 100
    assert result[1]["score"] == 100
    assert result[2]["score"] == 90
```

Then fix deterministically and re-run tests repeatedly to confirm stability.

---

## Quick anti-pattern matrix

| Principle | Anti-pattern | Corrective behavior |
|---|---|---|
| Think Before Coding | Silent assumptions | Ask clarifying questions and list assumptions |
| Simplicity First | Premature abstractions | Build smallest working solution |
| Surgical Changes | Unrelated edits and refactors | Restrict edits to request-relevant lines |
| Goal-Driven | "Done" without proof | Define and run explicit verification checks |

---

## Usage boundary examples

Use strict full protocol:

- Ambiguous requirements
- High-risk paths (auth/payments/data)
- Multi-file changes
- Refactors with behavior impact

Use lightweight protocol:

- Obvious typo and copy edits
- Single-line deterministic fixes

Even in lightweight mode, do not violate:

- No unrequested features
- No unrelated edits
- No unverifiable claims
