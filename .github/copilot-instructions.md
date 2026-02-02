# .github/copilot-instructions.md
# Tenx MCP AI Agent Rules File for GitHub Copilot

## Purpose
This file guides GitHub Copilot to follow my coding style, best practices, and interaction preferences.  
It ensures generated code aligns with my intent and project expectations.

---

## 1. General Behavior
- Always ask clarifying questions before generating code if instructions are ambiguous.
- Provide reasoning in comments for any suggestions or code changes.
- Avoid generating large code blocks without confirming context first.

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
- Use **Jest** as the testing framework.
- Include edge cases and example inputs/outputs in test cases.

---

## 4. Documentation & Formatting
- Use markdown code blocks when showing code.
- Include docstrings or comments explaining each function or class.
- Prioritize readable, maintainable code over clever shortcuts.

---

## 5. Interaction Preferences
- Wait for user confirmation before suggesting architecture-level changes.
- Provide multiple options only when explicitly requested.
- If code references external libraries or APIs, explain why they are chosen.

---

## 6. Error Handling
- Include proper error handling and input validation.
- Throw descriptive errors when necessary, not generic messages.

---

## 7. Iterative Learning
- Adapt to my coding patterns over time.
- Remember my preferences for language, style, and testing approach.
- Flag any deviation from previous instructions.

---

## 8. Logging & Summaries
- For each generated code block, include a short summary of:
  - What the code does
  - Any assumptions made
  - Recommendations for improvement

---

### Example Prompt & Expected Response
**Prompt:** “Create a function to fetch user data from an API.”

**Copilot Response Example:**
```typescript
// Fetches user data from API endpoint /users/:id
// Assumes API returns JSON: {id, name, email}
// Throws error if fetch fails or data is invalid

async function fetchUserData(userId: string): Promise<User> {
  if (!userId) throw new Error("User ID must be provided");

  const response = await fetch(`/users/${userId}`);
  if (!response.ok) throw new Error(`API request failed: ${response.status}`);

  const data = await response.json();
  return data as User;
}

// Jest unit test
test('fetchUserData returns user data for valid ID', async () => {
  const mockData = { id: '123', name: 'Alice', email: 'alice@example.com' };
  global.fetch = jest.fn(() => Promise.resolve({ ok: true, json: () => Promise.resolve(mockData) })) as any;

  const result = await fetchUserData('123');
  expect(result).toEqual(mockData);
});
