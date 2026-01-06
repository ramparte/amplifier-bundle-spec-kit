---
bundle:
  name: spec-implementer
  version: 1.0.0
  description: "Implement code from specifications and plans"
  author: "Amplifier Team"
  license: MIT
  repository: https://github.com/ramparte/amplifier-bundle-spec-kit

includes:
  - bundle: git+https://github.com/microsoft/amplifier-foundation@main

agents:
  include:
    - spec-kit:implementer
---

@spec-kit:context/shared/spec-kit-base.md

# Spec Implementer Bundle

Implement code following specifications and plans.

## Usage

```bash
amplifier run --bundle spec-implementer "Implement the following spec..."
```
