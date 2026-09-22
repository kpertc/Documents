### Xcode Command Line Tools
```bash
xcode-select --install
```

Check if installed (prints the CLT path, non-zero exit if missing)
```bash
xcode-select -p
```

Check version
```bash
pkgutil --pkg-info=com.apple.pkg.CLTools_Executables
```

`xcode-select --version` only reports the xcode-select shim itself, which ships with macOS → it succeeds either way

Xcodes - Xcode 多版本管理工具
``` shell
brew install --cask xcodes
```

### CMake
[[cmake]]
```Shell
brew install cmake
```