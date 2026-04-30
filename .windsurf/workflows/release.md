---
description: Crear un nuevo release con changelog
---

# Release - Crear nueva versión

Crea un nuevo release de tauri-easy-updater con changelog y git tag.

## Pasos

// turbo
1. Asegurar que estamos en main y todo está commit:
   ```bash
   git checkout main
   git pull origin main
   git status
   ```

// turbo
2. Verificar tests:
   ```bash
   pnpm install
   pnpm lint
   pnpm typecheck
   pnpm build
   cargo build --manifest-path crates/tauri-easy-updater/Cargo.toml
   ```

// turbo
3. Actualizar versión en todos los paquetes:
   - `package.json` (raíz) - versión del monorepo
   - `packages/core/package.json` - `@keyler_tamayo/tauri-easy-updater`
   - `packages/cli/package.json` - `@keyler_tamayo/tauri-easy-updater-cli`
   - `crates/tauri-easy-updater/Cargo.toml` - crate de Rust

   Usar semver: patch (0.0.1), minor (0.1.0), o major (1.0.0)

// turbo
4. Actualizar CHANGELOG.md con los cambios de la nueva versión

// turbo
5. Commit de versión:
   ```bash
   git add -A
   git commit -m "chore(release): vX.Y.Z"
   git push origin main
   ```

// turbo
6. Crear git tag:
   ```bash
   git tag -a "vX.Y.Z" -m "Release vX.Y.Z"
   git push origin "vX.Y.Z"
   ```

// turbo
7. Crear release en GitHub:
   - Ir a https://github.com/keylertamayo/tauri-easy-updater/releases
   - Click en "Draft a new release"
   - Seleccionar el tag creado
   - Agregar título: "vX.Y.Z"
   - Pegar contenido del CHANGELOG correspondiente
   - Publicar release

// turbo
8. Ejecutar deploy para npm/crates.io (opcional):
   - Ir a Actions > Publish
   - Run workflow
