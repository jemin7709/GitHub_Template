# GitHub Copilot Custom Instructions

## Core Principles & General Guidelines

1.  **Preserve Existing Code:** Carefully integrate generated code. **Do not erase or overwrite necessary existing code** unless specifically asked to refactor or replace it.
2.  **Safety & Security:** All code MUST use safe and secure practices. Avoid hardcoded secrets, passwords, API keys, insecure operations, and common vulnerabilities.
3.  **Efficiency & Quality:** Code MUST be optimized for algorithmic efficiency (time and space complexity) and follow language-specific style conventions (e.g., DRY principle). Avoid unnecessary code or technical debt.
4.  **Modularity:** Design code in reusable modules, components, or functions.
5.  **Readability & Maintainability:** Prioritize clear, well-commented, and maintainable code. Use comments to explain *why* specific design choices were made, especially for complex logic or optimizations. Explain algorithms used.
6.  **File Context:** Always provide the relevant filename (e.g., `utils.py`, `styles.css`) where the code snippet belongs.
7.  **Public Code Adaptation:** Avoid generating code verbatim from public examples. Modify public code significantly to avoid direct copying. If code is heavily based on a public source, inform the user with a note about its origin or inspiration.
8.  **Handle Edge Cases:** Explicitly consider and handle common edge cases (e.g., empty inputs, invalid data, null values). Use clear exception handling.
9.  **Dependencies:** When using external libraries, mention their purpose in comments.
10. **Testing:** Include comments suggesting relevant test cases, especially for critical paths and edge cases.

## Python Specific Instructions

1.  **Environment:** Assume Python projects are managed using `uv`. Use relevant `uv` commands if demonstrating setup or dependency management (e.g., `uv pip install <package>`, `uv run <command>`).
2.  **Style & Formatting:**
    *   Strictly follow **PEP 8**.
    *   Use 4 spaces for indentation.
    *   Keep lines under 80 characters where practical.
3.  **Syntax & Idioms:**
    *   Use modern Python 3.9+ syntax.
    *   Prefer f-strings for string formatting.
    *   Use `|` for union types (PEP 604) and dictionary merging (Python 3.9+).
    *   Use modern standard generics (e.g., `list[int]`, `dict[str, float]`) instead of `typing.List`, `typing.Dict` (PEP 585).
    *   Prefer `pathlib` over `os.path`.
    *   Use `itertools` for common iterator operations where applicable.
    *   Prefer duck-typing checks (`hasattr`) over `isinstance` where appropriate, but use `isinstance` for type safety when needed.
4.  **Type Hinting & Docstrings:**
    *   Use type annotations in all function/method signatures, unless the existing codebase explicitly avoids them.
    *   Do *not* add inline type hints for local variables if type inference is clear from assignment (e.g., `my_var: int = 5` is redundant, `my_var = 5` is sufficient).
    *   Write clear docstrings following **PEP 257** for all public modules, classes, functions, and methods.
    *   Provide clear comments within functions for complex logic.
5.  **File Handling:** When using `open()` in text mode, always specify `encoding='utf-8'`.
6.  **Command-Line Arguments:** Prefer `argparse` over `optparse`.
7.  **Logging:** When creating log statements, use the logging methods' argument placeholders (e.g., `logging.info("Processing item %s", item_id)`) instead of runtime string formatting (e.g., `logging.info(f"Processing item {item_id}")`).
8.  **Dummy Data:**
    *   Avoid generic placeholders like "Foo" or "Bar". Use creative, contextually relevant examples.
    *   Include diverse examples in strings (e.g., names, locations) using various languages (like English, Spanish, Mandarin, Hindi) where appropriate.
9.  **Code Generation:** Do not include example usage calls after generating a function, class, or standalone snippet unless specifically requested.
10. **OpenAI SDK (v1.0+):**
    *   **Embeddings:** Instantiate `client = OpenAI()`, then call `response = client.embeddings.create(model="...", input=..., dimensions=...)`. The embedding is in `response.data[0].embedding`.
    *   **Chat Completions:** Instantiate `client = OpenAI()`, then call `response = client.chat.completions.create(messages=..., model="...", ...)`. The content is in `response.choices[0].message.content`.

## Bicep Specific Instructions

1.  **Naming:** Use `lowerCamelCase` for parameters, variables, and resource symbolic names.
2.  **Symbolic Names:** Use descriptive symbolic names for resources (e.g., `appServicePlan`, `storageAccount`).
3.  **Parameters:** Declare all parameters at the top of the file with `@description` decorators.
4.  **API Versions:** Use the latest *stable* API versions for resources.
5.  **References:** Use symbolic names for resource references (e.g., `storageAccount.id`, `virtualNetwork.properties.addressSpace`). Avoid `reference()` and `resourceId()` functions where possible.
6.  **Dependencies:** Define dependencies implicitly via symbolic name references, not explicit `dependsOn`.
7.  **Outputs:** Never include secrets or keys in outputs. Refer to resource properties directly (e.g., `output endpoint string = storageAccount.properties.primaryEndpoints.web`).

## HTML/CSS Specific Instructions

1.  **JavaScript Separation:** When making AJAX requests or performing other dynamic actions, keep JavaScript logic in separate `.js` files. Do not embed complex JavaScript directly within `<script>` tags in HTML or use inline event handlers (e.g., `onclick="..."`) extensively.