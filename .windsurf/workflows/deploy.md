---
description: Publicar paquetes en npm y crates.io
---

# Deploy - Publicar tauri-easy-updater

Publica los paquetes npm (`@meacore/tauri-easy-updater` y `@meacore/tauri-easy-updater-cli`) y el crate de Rust en crates.io.

## Requisitos previos

Asegúrate de tener configurados estos secrets en GitHub:

### NPM_TOKEN (⚠️ Requiere configuración especial si tienes 2FA)

Si tienes 2FA habilitado en npm, debes crear un **Granular Access Token** con "Bypass 2FA":

1. Ve a https://www.npmjs.com/settings/tokens
2. Click en "Generate New Token" > "Granular Access Token"
3. Configura:
   - **Name**: `github-actions-publish`
   - **Packages and scopes**: Read and write para:
     - `@meacore/tauri-easy-updater`
     - `@meacore/tauri-easy-updater-cli`
   - **⚠️ IMPORTANTE**: Marca "Bypass 2FA for this token"
4. Copia el token y guárdalo en GitHub Secrets como `NPM_TOKEN`

**Nota**: Si ves el error `403 Forbidden - Two-factor authentication... required`, tu token no tiene el bypass 2FA habilitado.

### CARGO_REGISTRY_TOKEN
1. Ve a https://crates.io/settings/tokens
2. Click en "New Token"
3. Selecciona scope: **publish-update**
4. Guarda el token en GitHub Secrets como `CARGO_REGISTRY_TOKEN`

## Pasos

// turbo
1. Verificar que los tests pasan:
   ```bash
   pnpm install
   pnpm lint
   pnpm typecheck
   pnpm build
   cargo build --manifest-path crates/tauri-easy-updater/Cargo.toml
   ```

// turbo
2. Actualizar versión en los package.json y Cargo.toml si es necesario

// turbo
3. Crear git tag para la versión:
   ```bash
   VERSION=$(node -p "require('./package.json').version")
   git tag -a "v$VERSION" -m "Release v$VERSION"
   git push origin "v$VERSION"
   ```

// turbo
4. Ejecutar el workflow de GitHub Actions para publicar:
   - Ir a GitHub > Actions > Publish
   - Click en "Run workflow"
   - Seleccionar la rama main
   - Ejecutar

## Verificación manual (alternativa)

Si prefieres publicar manualmente en lugar de usar GitHub Actions:

// turbo
5. Publicar en npm:
   ```bash
   pnpm build
   cd packages/core && npm publish --access public
   cd ../cli && npm publish --access public
   ```

// turbo
6. Publicar en crates.io:
   ```bash
   cargo publish --manifest-path crates/tauri-easy-updater/Cargo.toml
   ```

## Verificación post-deploy

// turbo
7. Verificar que los paquetes están disponibles:
   ```bash
   npm view @meacore/tauri-easy-updater
   npm view @meacore/tauri-easy-updater-cli
   cargo search tauri-easy-updater
   ```
