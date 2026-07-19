
# Agent Test Spec: cocos-shader-specialist

## Agent Summary

Domain: Cocos Creator rendering — Cocos Effect files (.effect), material system, particle systems, post-processing, and rendering performance.
Model tier: Sonnet (default).
No gate IDs assigned.

---

## Static Assertions (Structural)

- [ ] `description:` field is present and domain-specific (references Cocos Effect / materials / rendering pipeline)
- [ ] `allowed-tools:` list includes Read, Write, Edit, Bash, Glob, Grep
- [ ] Model tier is Sonnet (default for specialists)
- [ ] Agent definition covers both 2D sprite shaders and 3D surface shaders

---

## Test Cases

### Case 1: Custom dissolve shader

**Input:** "Create a 2D sprite dissolve effect where the sprite dissolves based on a noise texture."
**Expected behavior:**

- Produces a complete `.effect` file with YAML header and GLSL shader code
- Includes: `noiseTexture` uniform, `dissolveThreshold` with range hint, `edgeColor` for edge glow
- Uses `discard` for pixels below threshold
- Comments explain each section of the effect
- Notes performance implications of `discard` on mobile

### Case 2: Material property manipulation

**Input:** "How do I change a material's color at runtime in TypeScript?"
**Expected behavior:**

- Shows `material.setProperty('mainColor', new Color(255, 0, 0, 255))` pattern
- Warns about shared material instances — use `MaterialVariant` or clone
- Explains the difference between shared and instance materials
- Provides complete code example with proper null checks

### Case 3: Particle system optimization

**Input:** "Our particle system is causing frame drops on mobile. What should I check?"
**Expected behavior:**

- Provides a diagnostic checklist:
  - Total particle count (target < 200 per system on mobile)
  - Particle lifetime (reduce to minimum needed)
  - Texture size and format
  - Culling mode configuration
  - Whether systems auto-play when off-screen
- Provides specific settings to adjust
- Recommends profiling with Cocos Creator's built-in tools

### Case 4: Post-processing setup

**Input:** "Add a bloom effect to the main camera."
**Expected behavior:**

- Shows how to configure Camera component's post-processing settings
- Provides the correct bloom threshold, intensity, and iteration settings
- Notes the performance cost of bloom on different platforms
- Suggests platform-specific adjustments

### Case 5: Draw call optimization

**Input:** "Our UI has 200+ draw calls. How do I reduce them?"
**Expected behavior:**

- Identifies common causes of high draw calls in Cocos Creator UI
- Recommends: Sprite Atlas usage, UIStaticBatch for static elements, reducing material variants
- Provides before/after analysis
- Sets target draw call counts for different platforms

---

## Protocol Compliance

- [ ] Produces complete .effect files with YAML + GLSL structure
- [ ] Includes performance notes for mobile targets
- [ ] References Cocos Creator's rendering pipeline documentation
- [ ] Provides platform-specific considerations
- [ ] Stays within shader/rendering domain

---

## Coverage Notes

- Dissolve shader (Case 1) tests the agent's ability to produce complete, working .effect files
- Material manipulation (Case 2) tests runtime API knowledge
- Draw call optimization (Case 5) verifies practical performance knowledge
