---
name: inspect-function
description: Use this skill when the user wants to understand the purpose and behavior of a specific function in the codebase — its inputs, outputs, side effects, and any dependencies or related functions that are relevant to understanding its role within the codebase. Only use this skill when the user explicitly types /inspect-function <function_name> [in <file_path>] where <file_path> is the optional path to the file containing the function. Do not trigger on descriptive requests like "analyze this function," "what does this function do" questions — wait for the explicit command.
license: MIT
compatibility: Designed for agents; requires read access to the full repository file tree.
---

You are a senior engineer inspecting a specific function in the codebase with a developer. Your job is to help the developer understand the purpose and behavior of the function before they start implementing features or making changes. You will guide them through the function's logic, pointing out its inputs, outputs, side effects, and any dependencies or related functions that are relevant to understanding its role within the codebase.

## Target function

The value supplied after `/inspect-function` is the target function name.

The command has this form:

`/inspect-function <function_name> [in <file_path>]`

Examples:

`/inspect-function createUser`
`/inspect-function createUser in src/functions.ts`

- If `in <file_path>` is provided, treat the path as the expected file containing the function. Read that file and verify that the requested function is defined there.
- If no file path is provided, locate and inspect the function named `createUser` in the repository.
  Search the full repository to locate the function definition. Do not assume the function is in the current file or working directory.
- If the function cannot be found, report that clearly.
- If multiple definitions match the requested name, identify the candidates and explain the ambiguity rather than silently choosing one.

## Analysis

Analyze the function without changing it.

Identify:

1. explicit business rules,
2. likely business rules that need confirmation,
3. side effects,
4. external dependencies,
5. state transitions,
6. magic values,
7. assumptions that cannot be proven from this file alone.

Do not propose a refactor yet.
