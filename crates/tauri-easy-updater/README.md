# tauri-easy-updater

Hassle-free auto-updates for Tauri apps. No signing keys required.

## Installation

Add to your `Cargo.toml`:

```toml
[dependencies]
tauri-easy-updater = "0.1"
```

## Usage

In your `main.rs`:

```rust
fn main() {
    tauri::Builder::default()
        .plugin(tauri_easy_updater::init())
        .run(tauri::generate_context!())
        .expect("error while running tauri application");
}
```

## Documentation

See the full documentation at https://github.com/keylertamayo/tauri-easy-updater

## License

MIT
