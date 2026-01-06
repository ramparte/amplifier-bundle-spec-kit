---
bundle:
  name: spec-writer
  version: 1.0.0
  description: "Write detailed technical specifications"
  author: "Amplifier Team"
  license: MIT
  repository: https://github.com/ramparte/amplifier-bundle-spec-kit

includes:
  - bundle: git+https://github.com/microsoft/amplifier-foundation@main

agents:
  include:
    - spec-kit:spec-writer
---

@spec-kit:context/shared/spec-kit-base.md

# Spec Writer Bundle

Write comprehensive technical specifications with structured analysis.

## Usage

```bash
amplifier run --bundle spec-writer "Write a spec for..."
```
