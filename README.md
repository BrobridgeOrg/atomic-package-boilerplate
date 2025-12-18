# Atomic Package Boilerplate

A boilerplate template for creating Atomic packages.

## Overview

This repository provides a minimal starting point for creating your own Atomic packages. Atomic packages are self-contained, versioned software packages that can be deployed and managed independently.

## What's Included

- `manifest.json` - Package configuration file
- `LICENSE` - Apache 2.0 license
- Basic directory structure

## Manifest Configuration

The `manifest.json` file defines your package's metadata and configuration:

```json
{
  "name": "your-package-name",
  "version": "0.0.1",
  "node_modules": "$PKG_PATH/node_modules",
  "override_env": {
    "YOUR_ENV_VAR": "value"
  },
  "ld_library_path": ["$PKG_PATH/lib"]
}
```

### Manifest Fields

- **name**: The unique identifier for your package
- **version**: Semantic version number (e.g., 1.0.0)
- **node_modules**: Path to Node.js dependencies (uses `$PKG_PATH` variable)
- **override_env**: Environment variables to set when the package is loaded
- **ld_library_path**: Array of paths for shared library loading

## Getting Started

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd atomic-package-boilerplate
   ```

2. Customize the `manifest.json`:
   - Update the `name` field with your package name
   - Adjust the `version` as needed
   - Add any environment variables your package requires
   - Configure library paths if needed

3. Add your package content:
   - Create a `lib/` directory for shared libraries
   - Create a `node_modules/` directory for Node.js dependencies
   - Add your application code and assets

4. Build and package your atomic package according to your deployment requirements

## Directory Structure

```
atomic-package-boilerplate/
├── manifest.json       # Package configuration
├── LICENSE            # Apache 2.0 license
├── README.md          # This file
├── lib/               # (Optional) Shared libraries
└── node_modules/      # (Optional) Node.js dependencies
```

## Environment Variables

The `$PKG_PATH` variable is automatically set to the package installation directory and can be used in your manifest configuration to reference package-relative paths.

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome. Please feel free to submit issues or pull requests.