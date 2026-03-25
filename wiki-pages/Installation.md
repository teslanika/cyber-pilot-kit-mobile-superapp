# Installation

## Requirements

- [Cyber Pilot](https://github.com/cyberfabric/cyber-pilot) CLI installed
- Git repository for your project

## Install the Kit

```bash
# Install latest version
cpt kit install teslanika/cyber-pilot-kit-mobile-superapp

# Install specific version
cpt kit install teslanika/cyber-pilot-kit-mobile-superapp --version 1.0.0
```

## Update

```bash
cpt kit update mobile-superapp
```

## Validate Installation

```bash
cpt validate-kits .
```

## Project Structure After Installation

```
your-project/
├── cypilot/
│   ├── .core/                    # Cypilot core (auto-managed)
│   ├── .gen/
│   │   └── kits/
│   │       └── mobile-superapp/  # Installed kit
│   └── config/
│       └── artifacts.toml        # Your artifact registry
```

## Configuration

After installation, configure your project in `cypilot/config/artifacts.toml`:

```toml
version = "1.0"
project_root = ".."

[kits.mobile-superapp]
format = "Cypilot"
path = ".gen/kits/mobile-superapp"

[[systems]]
name = "My SuperApp"
slug = "myapp"
kit = "mobile-superapp"
artifacts_dir = "architecture"
```

## Next Steps

1. [Create your first Platform PRD](4-Level-Hierarchy#l0-platform)
2. [Understand the hierarchy](4-Level-Hierarchy)
3. [Learn ID naming conventions](ID-Naming-Conventions)
