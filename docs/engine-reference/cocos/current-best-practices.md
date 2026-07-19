
# Cocos Creator — Current Best Practices

Last verified: [TO BE CONFIGURED]

Practices that are correct for Cocos Creator 3.7+ but may not appear in older
tutorials or the LLM's training data.

## Component Architecture

- Use `@ccclass('ClassName')` with string name for all components — required for serialization
- Use `@property({ type: CCInteger })` instead of `@property(Number)` for integer inspector fields
- Use `@property({ type: CCFloat })` instead of `@property(Number)` for float inspector fields
- Use `@property({ type: CCBoolean })` for boolean inspector fields
- Always use `@requireComponent` when a component depends on another
- Prefer composition over inheritance — attach multiple small components to a node

## Asset Management

- Use `assetManager.loadBundle()` for modular asset loading
- Use `bundle.load()` / `bundle.loadDir()` for loading from specific bundles
- Use `resources.load()` only for core always-needed assets
- Release unused assets with `assetManager.releaseAsset()` to manage memory
- Configure sprite atlas for UI and 2D sprites to reduce draw calls

## TypeScript Patterns

- Use `import { _decorator, Component, Node } from 'cc'` — destructured imports
- Use `const { ccclass, property } = _decorator` — standard pattern
- Use `private _field: Type | null = null` for component references loaded in `onLoad()`
- Use `readonly` for constants and immutable properties
- Avoid `any` — use `unknown` with type guards when type is truly unknown

## UI System

- Use `Widget` component for all multi-resolution adaptation
- Use `cc.Tween` (imported as `tween`) for all UI animations
- Use `NodePool` for dynamic list item recycling
- Use `UIStaticBatch` for static UI elements to reduce draw calls
- Use `UIOpacity` for fade effects instead of per-node opacity
- Disable `raycastTarget` on non-interactive graphical elements

## Rendering

- Use Cocos Effect (`.effect`) format with `CCEffect %{}%` + `CCProgram` blocks
- Use `#include <cc-global>` for engine built-in uniforms
- Use `material.setProperty('name', value)` for runtime material changes
- Use `MaterialVariant` for slight material variations without duplicating effects
- Set texture compression per platform: ETC2 for Android, ASTC for iOS, DXT for desktop
