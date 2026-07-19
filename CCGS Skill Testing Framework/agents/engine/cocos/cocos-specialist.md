
# Agent Test Spec: cocos-specialist

## Agent Summary

Domain: Cocos Creator-specific patterns, component architecture, node/scene management, asset bundles, and TypeScript integration decisions.
Does NOT own: actual TypeScript code authoring (delegates to cocos-typescript-specialist).
Model tier: Sonnet (default).
No gate IDs assigned.

---

## Static Assertions (Structural)

- [ ] `description:` field is present and domain-specific (references Cocos Creator architecture / component patterns / engine decisions)
- [ ] `allowed-tools:` list includes Read, Write, Edit, Bash, Glob, Grep
- [ ] Model tier is Sonnet (default for specialists)
- [ ] Agent definition references `docs/engine-reference/cocos/VERSION.md` as the authoritative API source

---

## Test Cases

### Case 1: In-domain request — appropriate output

**Input:** "When should I use a Component vs. a plain TypeScript class in Cocos Creator?"
**Expected behavior:**

- Produces a pattern decision guide with rationale:
  - Component: needs lifecycle hooks (onLoad, start, update), needs to attach to a Node, needs inspector properties
  - Plain class: pure data/logic, no Node dependency, reusable across contexts, singleton managers
- Provides concrete examples of each pattern
- Does NOT produce raw code for both patterns — refers to cocos-typescript-specialist for implementation
- Notes the composition-over-inheritance principle

### Case 2: Wrong-engine redirect

**Input:** "Write a Godot script using @onready and _process(delta)."
**Expected behavior:**

- Does NOT produce Godot GDScript code
- Clearly identifies that this is a Godot pattern, not a Cocos Creator pattern
- Provides the Cocos Creator equivalent: `@property` + `onLoad()` + `update(dt)`
- Confirms the project is Cocos Creator-based and redirects the conceptual mapping

### Case 3: Post-cutoff API risk

**Input:** "Use the new Cocos Creator 3.9 render pipeline API to set up a custom render pass."
**Expected behavior:**

- Identifies that the API may be post-cutoff (introduced after LLM knowledge cutoff)
- Flags the version risk: LLM knowledge may be incomplete or incorrect
- Directs the user to verify against `docs/engine-reference/cocos/VERSION.md`
- Provides best-effort guidance while clearly marking it as unverified

### Case 4: Asset bundle strategy

**Input:** "Our game has 50 levels with unique assets. How should we organize asset bundles?"
**Expected behavior:**

- Provides a structured analysis:
  - Core bundle: shared assets (UI, common prefabs, fonts)
  - Per-chapter bundles: group 5-10 levels together
  - Remote bundles: optional content (DLC, seasonal events)
- Discusses trade-offs: bundle size vs. load frequency vs. memory
- Does NOT make the final decision unilaterally
- Defers the decision to `lead-programmer` with the analysis as input

### Case 5: Cross-platform deployment

**Input:** "We're targeting Web, iOS, and Android. What build configurations should I use?"
**Expected behavior:**

- Reads the project's target platform context
- Recommends platform-specific settings:
  - Web: WebAssembly, compressed textures, smaller bundles
  - iOS: Metal renderer, ASTC compression, App Store compliant
  - Android: Vulkan/GLES3, ETC2 compression, APK/AAB
- References Cocos Creator's build template system
- Notes any platform-specific limitations

---

## Protocol Compliance

- [ ] Stays within declared domain (Cocos Creator architecture decisions, component patterns, asset bundles)
- [ ] Redirects language-specific implementation to cocos-typescript-specialist
- [ ] Returns structured findings (decision trees, pattern recommendations with rationale)
- [ ] Treats `docs/engine-reference/cocos/VERSION.md` as authoritative over LLM training data
- [ ] Flags post-cutoff API usage with verification requirements
- [ ] Defers architecture decisions to lead-programmer when trade-offs exist

---

## Coverage Notes

- Component vs. plain class guide (Case 1) should be written as a reusable pattern doc
- Post-cutoff flag (Case 3) confirms the agent does not confidently use APIs it cannot verify
- Cross-platform case (Case 5) verifies the agent applies platform-specific knowledge
