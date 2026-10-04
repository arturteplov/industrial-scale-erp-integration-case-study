# Hardware and interfaces

| Device / model | Interface used |
|---|---|
| VEST-250A12E | serial / vendor service |
| VN-1500-4 + IE-04 | DB9 / serial |
| PROK/VP static 200 kg / 50 g | serial-class interface |
| KELI XK3118T1 | DB9 / RS-232-class interface |

## Transport path

```text
scale / indicator
→ serial or USB-serial adapter
→ edge Windows workstation
→ serial-to-TCP bridge
→ private network
→ vendor weighing service
→ HTTP adapter
→ integration service
→ BAS/ERP workflow
```

## Data fields

- logical scale ID;
- source path;
- raw value;
- raw unit;
- normalized kilograms;
- capture timestamp;
- BAS/ERP linkage.

## Excluded deployment data

- workstation names;
- network addresses;
- live COM/workstation mappings;
- licence/install codes;
- production configuration;
- customer-specific internal paths.
