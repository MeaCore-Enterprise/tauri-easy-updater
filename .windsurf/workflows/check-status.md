---
description: Verificar estado de publicación en npm y crates.io
---

# Check Status - Verificar publicación

Verifica si los paquetes están publicados y muestra su versión actual.

## Verificar estado de npm

// turbo
1. Verificar `@meacore/tauri-easy-updater`:
   ```bash
   npm view @meacore/tauri-easy-updater versions --json
   ```

// turbo
2. Verificar `@meacore/tauri-easy-updater-cli`:
   ```bash
   npm view @meacore/tauri-easy-updater-cli versions --json
   ```

## Verificar estado de crates.io

// turbo
3. Verificar `tauri-easy-updater` crate:
   ```bash
   curl -s https://crates.io/api/v1/crates/tauri-easy-updater | grep -o '"max_stable_version":"[^"]*"'
   ```

## Comparar versiones locales vs publicadas

// turbo
4. Mostrar versiones locales:
   ```bash
   echo "=== Local versions ==="
   echo "Core: $(node -p "require('./packages/core/package.json').version")"
   echo "CLI: $(node -p "require('./packages/cli/package.json').version")"
   echo "Crate: $(grep '^version' crates/tauri-easy-updater/Cargo.toml | head -1 | cut -d'"' -f2)"
   ```

// turbo
5. Mostrar versiones publicadas:
   ```bash
   echo "=== Published versions ==="
   echo "Core npm: $(npm view @meacore/tauri-easy-updater version 2>/dev/null || echo 'NOT PUBLISHED')"
   echo "CLI npm: $(npm view @meacore/tauri-easy-updater-cli version 2>/dev/null || echo 'NOT PUBLISHED')"
   echo "Crate: $(curl -s https://crates.io/api/v1/crates/tauri-easy-updater | grep -o '"max_stable_version":"[^"]*"' | cut -d'"' -f4)"
   ```

## Interpretación

- Si muestra **NOT PUBLISHED**: Los paquetes no están publicados aún. Necesitas configurar los secrets en GitHub y ejecutar el workflow de publish.
- Si muestra una **versión**: El paquete está publicado. Compara con la versión local para ver si necesitas hacer un nuevo release.

## Próximos pasos

Si los paquetes no están publicados:
- Configura `NPM_TOKEN` y `CARGO_REGISTRY_TOKEN` en GitHub Secrets
- Ejecuta el workflow de publish o usa `/deploy`

Si las versiones locales son mayores que las publicadas:
- Crea un nuevo release con `/release`
