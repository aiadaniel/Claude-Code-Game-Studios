
# Agent Test Spec: cocos-ui-specialist

## Agent Summary

Domain: Cocos Creator UI — component hierarchy, multi-resolution adaptation, screen management, UI animation, and UI performance.
Model tier: Sonnet (default).
No gate IDs assigned.

---

## Static Assertions (Structural)

- [ ] `description:` field is present and domain-specific (references UI components / multi-resolution / screen management)
- [ ] `allowed-tools:` list includes Read, Write, Edit, Bash, Glob, Grep
- [ ] Model tier is Sonnet (default for specialists)
- [ ] Agent definition covers both Widget-based layout and Canvas rendering modes

---

## Test Cases

### Case 1: Multi-resolution adaptation

**Input:** "Our UI looks great at 1920x1080 but breaks on phones. How do I fix this?"
**Expected behavior:**

- Explains Canvas design resolution and fit modes (fitHeight, fitWidth)
- Shows Widget component usage for anchoring UI elements
- Provides specific Widget settings for common layout patterns (top bar, bottom bar, center content)
- Recommends testing on common aspect ratios (16:9, 19.5:9, 4:3)
- Includes code examples for programmatic Widget setup

### Case 2: Screen management system

**Input:** "Design a screen manager that handles stacking screens (like a mobile app)."
**Expected behavior:**

- Produces a UIManager singleton pattern
- Shows screen stack management (push/pop)
- Includes base UIScreen class with onShow/onHide lifecycle
- Handles data passing between screens
- Notes how to handle back button / escape key for screen stack

### Case 3: UI animation

**Input:** "Make a dialog box that scales in from zero with a bounce effect."
**Expected behavior:**

- Uses `cc.Tween` API (not manual update() interpolation)
- Shows the complete tween chain: scale 0 → 1.2 → 1.0
- Includes easing functions (`backOut`, `sineOut`)
- Notes the importance of disabling interaction during animation
- Provides cleanup (stop tweens in onDestroy)

### Case 4: Dynamic scrollable list

**Input:** "Create an inventory list that can display 100+ items efficiently."
**Expected Behavior:**

- Recommends object pooling with `NodePool` for list items
- Shows ScrollView + Layout component setup
- Provides DynamicList component with pool management
- Handles item recycling on scroll
- Notes performance targets (instantiation time, memory usage)

### Case 5: UI performance audit

**Input:** "Audit this UI scene for performance issues." (scene with deep nesting, many Labels, no sprite atlas)
**Expected behavior:**

- Identifies: deep node nesting, missing Sprite Atlas, excessive Label updates
- Flags: `raycastTarget` on non-interactive elements
- Recommends: flattening hierarchy, using UIStaticBatch, adding Sprite Atlas
- Provides specific before/after metrics
- Notes the Canvas render mode implications

---

## Protocol Compliance

- [ ] Uses cc.Tween for all UI animations (never manual update() interpolation)
- [ ] Enforces Widget usage for multi-resolution support
- [ ] Recommends object pooling for dynamic lists
- [ ] Provides performance optimization guidance
- [ ] Stays within UI domain

---

## Coverage Notes

- Multi-resolution case (Case 1) tests the most common Cocos Creator UI challenge
- Screen manager case (Case 2) tests architecture design capability
- Performance audit (Case 5) verifies the agent can identify real-world UI performance issues
