# Failure modes

| Failure | Detection | Result | Recovery |
|---|---|---|---|
| Scale unavailable | read/vendor error | quantity unchanged | manual device check if persistent |
| Vendor timeout | request timeout | previous weight not reused | new acquisition on next attempt |
| Malformed response | response validation | measurement rejected | none |
| Wrong scale | device/path mismatch | measurement rejected | mapping review |
| Gross/tare inconsistency | arithmetic guard | transaction step rejected | input/physical-state correction |
| Duplicate request | operation identity / audit | replay or conflict rejection | no second business write |
| Integration service failure | HTTP health probe | workflow unavailable | bounded service restart |
| Vendor scale-service failure | synthetic application probe | scale read unavailable | bounded service restart |
| Public dashboard route failure | public HTTPS probe | weighing path remains local | restart once → route reapply once → cooldown |
| BAS/ERP sync stale | age of last success marker | dashboard coverage stale/unavailable | one bounded retry |
| Windows account password reset | Task Scheduler logon error | scheduled job does not start | credential refresh |
| DPAPI credential invalidation | decrypt failure | BAS sync stops | credential recreation + sync test |
| COM/USB absent | device not present | scale path unavailable | manual hardware handling |
| Licence invalid | vendor licence error | scale integration unavailable | manual licence handling |
| SQLite integrity failure | integrity check | state preserved | manual recovery; no automatic overwrite |

## Watchdog sequence

```text
probe
→ repeated failure threshold
→ dependency check
→ recovery action 1
→ retest
→ optional recovery action 2
→ retest
→ cooldown / manual handling
```
