
# Cocos Creator — Deprecated APIs

Last verified: [TO BE CONFIGURED]

## Deprecated in 3.8

| Old API | New API | Notes                            |
| ------- | ------- | -------------------------------- |
| —      | —      | No deprecations confirmed in 3.8 |

## Deprecated in 3.7

| Old API                  | New API                 | Notes                                      |
| ------------------------ | ----------------------- | ------------------------------------------ |
| `cc.js.getClassName()` | `js.getClassName()`   | Import from`cc` directly                 |
| `director._scene`      | `director.getScene()` | Use public API instead of private property |

## Deprecated in 3.6

| Old API                          | New API                                              | Notes                                   |
| -------------------------------- | ---------------------------------------------------- | --------------------------------------- |
| `resources.loadDir()`          | `assetManager.loadBundle()` + `bundle.loadDir()` | Use asset bundles for directory loading |
| `cc.assetManager.loadRemote()` | `assetManager.loadRemote()`                        | Remove`cc.` prefix                    |

## Long-Deprecated (Still Functional but Avoid)

| Old API                            | New API                        | Notes                                                |
| ---------------------------------- | ------------------------------ | ---------------------------------------------------- |
| `cc.find()`                      | `@property(Node)` references | Performance anti-pattern; use direct references      |
| `getComponent()` in `update()` | Cache in`onLoad()`           | Not deprecated but performance-critical anti-pattern |
| `any` type                       | Proper TypeScript interfaces   | Enforced by project coding standards                 |
