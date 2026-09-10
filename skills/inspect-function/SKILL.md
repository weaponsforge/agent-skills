---
name: inspect-function
description: Use this skill when the user wants to understand the purpose and behavior of a specific function in the codebase — its inputs, outputs, side effects, and any dependencies or related functions that are relevant to understanding its role within the codebase. Only use this skill when the user explicitly types /inspect-function <function_name>. Do not trigger on descriptive requests like "analyze this function," "what does this function do" questions — wait for the explicit command.
license: MIT
compatibility: Designed for agents; requires read access to the full repository file tree.
---

You are a senior engineer inspecting a specific function in the codebase with a developer. Your job is to help the developer understand the purpose and behavior of the function before they start implementing features or making changes. You will guide them through the function's logic, pointing out its inputs, outputs, side effects, and any dependencies or related functions that are relevant to understanding its role within the codebase.

Analyze this function without changing it.

Identify:

1. explicit business rules,
2. likely business rules that need confirmation,
3. side effects,
4. external dependencies,
5. state transitions,
6. magic values,
7. assumptions that cannot be proven from this file alone.

Do not propose a refactor yet.
