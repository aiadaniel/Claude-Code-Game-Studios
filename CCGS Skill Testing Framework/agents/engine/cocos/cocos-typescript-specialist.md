
# Agent Test Spec: cocos-typescript-specialist

## Agent Summary

Domain: TypeScript code quality in Cocos Creator — decorator patterns, component lifecycle, type safety, module organization, and TypeScript-specific optimization.
Model tier: Sonnet (default).
No gate IDs assigned.

---

## Static Assertions (Structural)

- [ ] `description:` field is present and domain-specific (references TypeScript patterns / Cocos Creator component lifecycle)
- [ ] `allowed-tools:` list includes Read, Write, Edit, Bash, Glob, Grep
- [ ] Model tier is Sonnet (default for specialists)
- [ ] Agent definition enforces strict TypeScript typing (no `any` usage)

---

## Test Cases

### Case 1: TypeScript strictness enforcement

**Input:** "Here's a component with untyped variables — review it." (code with `any` types and missing return types)
**Expected behavior:**

- Flags all untyped variables and missing return types
- Provides specific typed replacements
- Explains WHY each type annotation matters (maintainability, IDE support, refactoring safety)
- Does NOT rewrite the entire component — only the typing issues

### Case 2: Component lifecycle correctness

**Input:** "I'm calling `getComponent()` in `update()` to access another component — is this OK?"
**Expected behavior:**

- Identifies this as a performance anti-pattern
- Explains the cost of `getComponent()` and why it shouldn't be in hot paths
- Provides the correct pattern: cache in `onLoad()`, use `@property` for inspector references
- Shows before/after code examples

### Case 3: Decorator pattern usage

**Input:** "How do I use `@property` correctly for different data types in Cocos Creator?"
**Expected behavior:**

- Provides a comprehensive guide for `@property` decorator usage:
  - Primitive types: `@property(CCInteger)`, `@property(CCFloat)`, `@property(CCBoolean)`
  - Node/Component references: `@property({ type: Node })`, `@property({ type: Prefab })`
  - Arrays: `@property({ type: [Node] })`, `@property({ type: [CCInteger] })`
  - Enum types: `@property({ type: Enum(MyEnum) })`
- Includes `tooltip`, `range`, `slide` editor hints
- Notes the `@requireComponent` and `@executeInEditMode` decorators

### Case 4: Memory leak prevention

**Input:** "Review this component for memory leaks." (code with registered event listeners but no cleanup)
**Expected behavior:**

- Identifies missing `onDestroy()` cleanup
- Flags event listeners that need `node.off()` / `director.off()`
- Flags `scheduleOnce` / `setTimeout` without cleanup
- Provides the corrected component with proper cleanup in `onDestroy()`

### Case 5: Module organization

**Input:** "Our `assets/scripts/` folder is getting messy. How should we organize TypeScript modules?"
**Expected behavior:**

- Recommends feature-based folder organization
- Shows a clean module structure with `core/`, `components/`, `gameplay/`, `ui/`, `data/`, `utils/`
- Recommends barrel exports (`index.ts`) for clean imports
- Warns about circular import issues and how to avoid them with `import type`

---

## Protocol Compliance

- [ ] Enforces strict TypeScript typing in all code reviews
- [ ] Flags `any` type usage and provides typed alternatives
- [ ] Checks component lifecycle correctness (onLoad caching, onDestroy cleanup)
- [ ] Provides before/after examples for anti-patterns
- [ ] References Cocos Creator API documentation for decorator patterns
- [ ] Stays within TypeScript/code quality domain

---

## Coverage Notes

- Lifecycle case (Case 2) verifies the agent catches the most common Cocos performance mistake
- Decorator case (Case 3) covers the full range of property types Cocos Creator supports
- Memory leak case (Case 4) confirms the agent enforces event listener cleanup
