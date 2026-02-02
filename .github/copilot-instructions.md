# CLAUDE.md
# Tenx MCP AI Agent Rules File

## Purpose
This rules file guides the AI agent to follow my coding style, best practices, and interaction preferences. 
It ensures that generated code aligns with my intent and project expectations.

---

## 1. General Behavior
- Always confirm ambiguous requirements before generating code.
- If unclear instructions are given, ask clarifying questions.
- Provide reasoning and explanation for your suggestions in comments.
- Do not generate large blocks of code without confirming context first.

---

## 2. Programming Language & Style
- Primary language: TypeScript
- Use **functional programming patterns** wherever possible.
- Follow **clean code principles**:
  - Meaningful variable and function names
  - Small, reusable functions
  - Consistent indentation and formatting
- Include **inline comments** explaining complex logic.

---

## 3. Testing
- Always provide **unit tests** for functions and modules you generate.
- Use the testing framework **Jest** unless otherwise specified.
- Include edge cases and example inputs/outputs in test cases.

---

## 4. Documentation & Formatting
- Use markdown code blocks when showing code.
- Include brief docstrings or comments explaining each function or class.
- Prefer readable, maintainable code over clever or overly compact code.

---

## 5. Interaction Preferences
- Wait for my confirmation before suggesting architecture-level changes.
- Provide multiple options only when explicitly requested.
- If code references external libraries or APIs, briefly explain why they are chosen.

---

## 6. Error Handling
- Include proper error handling and validation for inputs.
- Throw descriptive errors when necessary instead of generic messages.

---

## 7. Iterative Learning
- Adapt to my coding patterns over time.
- Remember my preferences for language, style, and testing approach during this session.
- Flag any deviation from previous instructions.

---

## 8. Logging
- Whenever generating code, include a short summary of:
  - What the code does
  - Any assumptions made
  - Recommendations for improvement

---

### Example Use:
**Prompt:** “Create a function to fetch user data from an API.”

**Agent Response:**
```typescript
// This function fetches user data from the API endpoint /users/:id
// Assumption: API returns JSON with keys {id, name, email}
// Throws an error if fetch fails or data is invalid

async function fetchUserData(userId: string): Promise<User> {
  if (!userId) throw new Error("User ID must be provided");

  const response = await fetch(`/users/${userId}`);
  if (!response.ok) throw new Error(`API request failed: ${response.status}`);

  const data = await response.json();
  return data as User;
}

// Jest unit test for fetchUserData
test('fetchUserData returns user data for valid ID', async () => {
  const mockData = { id: '123', name: 'Alice', email: 'alice@example.com' };
  global.fetch = jest.fn(() => Promise.resolve({ ok: true, json: () => Promise.resolve(mockData) })) as any;

  const result = await fetchUserData('123');
  expect(result).toEqual(mockData);
});
