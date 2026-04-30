# @keyler_tamayo/tauri-easy-updater-cli

CLI for generating and publishing manifests for tauri-easy-updater.

## Installation

```bash
npm install -g @keyler_tamayo/tauri-easy-updater-cli
```

## Usage

### Generate manifest

```bash
npx @keyler_tamayo/tauri-easy-updater-cli generate-manifest \
  --version 1.1.0 \
  --base-url "https://github.com/myuser/myapp/releases/download/v1.1.0"
```

### Upload manifest

```bash
npx @keyler_tamayo/tauri-easy-updater-cli upload-manifest \
  --version 1.1.0 \
  --token YOUR_GITHUB_TOKEN
```

## Documentation

See the full documentation at https://github.com/keylertamayo/tauri-easy-updater

## License

MIT
