# ZAPP

**Simplify your macOS App deployment**

Zapp is a powerful CLI tool designed to streamline the deployment process for macOS applications. With Zapp, you can effortlessly create DMG and PKG files, perform code signing, notarize your apps, and modify plist files.

## Features

- [x] Create DMG files
- [x] Create PKG files
- [ ] Code signing
- [ ] Notarization / Stapling with Retries
- [ ] Modify plist (version)
- [ ] Auto binary dependencies bundling
- [ ] Support GitHub Actions

## Installation

(TODO: Add installation instructions)

## Usage

### Creating DMG Files

Create a DMG file from the app bundle:

```bash
zapp dmg "<path of app-bundle>"
```

```bash
zapp dmg --title "My App" --out "MyApp.dmg" --icon "path/to/icon.icns" "path/to/target.app"
```

### Creating PKG Files

#### Create a PKG file from the app bundle
```bash
zapp pkg "<path of app-bundle>"
```

```bash
zapp pkg --out "MyApp.pkg" --version "1.2.3" --identifier "com.example.myapp" "<path of app-bundle>"
```

#### With EULA Files

Include End User License Agreement (EULA) files in multiple languages:

```bash
zapp pkg "<path of app-bundle>" --eula en:eula_en.txt,es:eula_es.txt,fr:eula_fr.txt
```

### Code Signing (Coming Soon)

```bash
zapp sign "<target app/dmg/pkg>"
```

## Advanced Usage

(TODO: Add advanced usage examples)

## Contributing

We welcome contributions to Zapp! Please see our [Contributing Guidelines](CONTRIBUTING.md) for more information.

## License

Zapp is released under the [MIT License](LICENSE).

## Support

If you encounter any issues or have questions, please file an issue on the [GitHub issue tracker](https://github.com/your-repo/zapp/issues).
