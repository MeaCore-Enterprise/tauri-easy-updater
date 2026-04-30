# @keyler_tamayo/tauri-easy-updater

Hassle-free auto-updates for Tauri apps. No signing keys required.

## Installation

```bash
npm install @keyler_tamayo/tauri-easy-updater
```

## Usage

```tsx
import {
  useUpdateChecker,
  UpdateBanner,
  createGitHubProvider,
} from '@keyler_tamayo/tauri-easy-updater';

function App() {
  const { updateInfo, dismiss } = useUpdateChecker({
    currentVersion: '1.0.0',
    provider: createGitHubProvider({ owner: 'myuser', repo: 'myapp' }),
  });

  return (
    <>
      {updateInfo?.hasUpdate && (
        <UpdateBanner updateInfo={updateInfo} onDismiss={dismiss} />
      )}
    </>
  );
}
```

## Documentation

See the full documentation at https://github.com/keylertamayo/tauri-easy-updater

## License

MIT
