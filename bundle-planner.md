---
bundle:
  name: spec-planner
  version: 1.0.0
  description: "Plan implementation from specifications"
  author: "Amplifier Team"
  license: MIT
  repository: https://github.com/ramparte/amplifier-bundle-spec-kit

includes:
  - bundle: git+https://github.com/microsoft/amplifier-foundation@main

agents:
  include:
    - spec-kit:planner
---

@spec-kit:context/shared/spec-kit-base.md

# Spec Planner Bundle

Create implementation plans from technical specifications.

## Usage

```bash
amplifier run --bundle spec-planner "Plan implementation for..."
```
