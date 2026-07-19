
# Cocos Creator — Breaking Changes

Last verified: [TO BE CONFIGURED]

## Version 3.7 → 3.8

### HIGH RISK

| Area         | Change                       | Impact                                                   | Migration                                   |
| ------------ | ---------------------------- | -------------------------------------------------------- | ------------------------------------------- |
| Build System | New build template structure | Custom build templates may need updating                 | Review`settings/v2/packages/builder.json` |
| Asset Bundle | Bundle loading API changes   | `assetManager.loadBundle()` callback signature updated | Check error-first callback pattern          |

### MEDIUM RISK

| Area      | Change                            | Impact                           | Migration                                |
| --------- | --------------------------------- | -------------------------------- | ---------------------------------------- |
| UI System | Widget component property renames | Some Widget properties renamed   | Search for old property names and update |
| Physics   | PhysX integration updates         | Physics material API adjustments | Review physics material creation code    |

### LOW RISK

| Area  | Change                         | Impact                                        | Migration                     |
| ----- | ------------------------------ | --------------------------------------------- | ----------------------------- |
| Tween | Internal tween system refactor | No API change, but timing may differ slightly | Regression test UI animations |

## Version 3.6 → 3.7

### MEDIUM RISK

| Area            | Change                                | Impact                                   | Migration                      |
| --------------- | ------------------------------------- | ---------------------------------------- | ------------------------------ |
| Render Pipeline | Forward pipeline improvements         | Custom render passes may need adjustment | Test custom effect files       |
| Node            | `cc.find()` performance degradation | Already discouraged, now slower          | Replace with direct references |
