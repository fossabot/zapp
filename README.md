# ZAPP
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fironpark%2Fzapp.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fironpark%2Fzapp?ref=badge_shield)


[**English**](README.md) | [한국어](README.ko.md) | [日本語](README.ja.md) 

**Simplify your macOS App deployment**

`zapp` is a powerful CLI tool designed to streamline and automate the deployment process for macOS applications. It handles all stages of deployment in one tool, from dependency bundling to DMG/PKG creation, code signing, and notarization.

## Features

- [x] Create DMG files
- [x] Create PKG files
- [x] Code signing
- [x] Notarization / Stapling
- [ ] Modify plist (version)
- [x] Auto binary dependencies bundling
- [ ] Support GitHub Actions

## Installation
Using Homebrew
```bash
brew tap ironpark/zapp
brew install zapp
```
Using Go
```bash
go install github.com/ironpark/zapp@latest
```

## Usage

### Full Example
The following is a complete example showing how to use `zapp` to dependency bundling, codesign, packaging, notarize, and staple `MyApp.app`:

```bash
# Dependency bundling
zapp dep --app="MyApp.app"

# Codesign / notarize / staple
zapp sign --target="MyApp.app"
zapp notarize --profile="key-chain-profile" --target="MyApp.app" --staple

# Create pkg/dmg file
zapp pkg --app="MyApp.app" --out="MyApp.pkg"
zapp dmg --app="MyApp.app" --out="MyApp.dmg"

# Codesign / notarize / staple for pkg/dmg
zapp sign --target="MyApp.app"
zapp sign --target="MyApp.pkg"

zapp notarize --profile="key-chain-profile" --target="MyApp.pkg" --staple
zapp notarize --profile="key-chain-profile" --target="MyApp.dmg" --staple
```
or just use the shorthand command
```bash
zapp dep --app="MyApp.app" --sign --notarize --staple

zapp pkg --out="MyApp.pkg" --app="MyApp.app" \ 
  --sign --notarize --profile="key-chain-profile" --staple

zapp dmg --out="MyApp.dmg" --app="MyApp.app" \
  --sign --notarize --profile="key-chain-profile" --staple
```

### Dependency Bundling
This process inspects the dependencies of the application executable, includes the necessary libraries within /Contents/Frameworks, and modifies the link paths to enable standalone execution.

```bash
zapp dep --app="path/to/target.app"
```
You can add additional paths to search for libraries
```bash
zapp dep --app="path/to/target.app" --libs="/usr/local/lib" --libs="/opt/homebrew/Cellar/ffmpeg/7.0.2/lib"
```


### Creating DMG Files

> Zapp can be used to create DMG files, a common format used for distributing macOS apps.
It greatly simplifies the DMG creation process by automatically extracting icons from the app bundle, compositing disk icons, and providing an interface for drag-and-drop installation of the app.


```bash
zapp dmg --app="path/to/target.app"
```

```bash
zapp dmg --title="My App" \ 
  --app="path/to/target.app" \
  --icon="path/to/icon.icns" \
  --bg="path/to/background.png" \ 
  --out="MyApp.dmg"
```

### Creating PKG Files

> [!NOTE]
> 
> If the `--version` and `--identifier` flags are not set, these values will be automatically retrieved from the Info.plist file of the provided app bundle

#### Create a PKG file from the app bundle
```bash
zapp pkg --app="path/to/target.app"
```

```bash
zapp pkg --out="MyApp.pkg" --version="1.2.3" --identifier="com.example.myapp" --app="path/to/target.app"
```

#### With EULA Files

Include End User License Agreement (EULA) files in multiple languages:

```bash
zapp pkg --eula=en:eula_en.txt,es:eula_es.txt,fr:eula_fr.txt --app="path/to/target.app" 
```
### Code Signing

If the `--identity` flag is not used to select a certificate, Zapp will automatically select an available certificate from the current keychain.

```bash
zapp sign --target="path/to/target.(app,dmg,pkg)"
```
```bash
zapp sign --identity="Developer ID Application" --target="path/to/target.(app,dmg,pkg)"
```

### Notarization & Stapling
> [!NOTE]
> 
> When executing the notarize command, if Zapp receives an app bundle path, it automatically compresses the app bundle and attempts to notarize it.

```bash
zapp notarize --profile="key-chain-profile" --target="path/to/target.(app,dmg,pkg)" --staple
```

```bash
zapp notarize --apple-id="your@email.com" --password="pswd" --team-id="XXXXX" --target="path/to/target.(app,dmg,pkg)" --staple
```

## License

Zapp is released under the [MIT License](LICENSE).


[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fironpark%2Fzapp.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fironpark%2Fzapp?ref=badge_large)

## Support

If you encounter any issues or have questions, please file an issue on the [GitHub issue tracker](https://github.com/ironpark/zapp/issues).