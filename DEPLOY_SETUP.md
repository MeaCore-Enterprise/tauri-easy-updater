# Configuración de Despliegue - tauri-easy-updater

Este documento describe cómo desplegar los paquetes de tauri-easy-updater.

## Estado Actual

Los paquetes **NO están publicados** aún en npm ni crates.io.

## Archivos Configurados

### GitHub Actions (existentes)
- `.github/workflows/test.yml` - CI para tests
- `.github/workflows/publish.yml` - Publicación automática

### Windsurf Workflows (creados)
- `.windsurf/workflows/deploy.md` - Comando `/deploy` para publicar
- `.windsurf/workflows/release.md` - Comando `/release` para crear versiones
- `.windsurf/workflows/check-status.md` - Comando `/check-status` para verificar estado

### Metadata de paquetes (actualizada)
- `packages/core/package.json` - Metadata npm para @meacore/tauri-easy-updater
- `packages/cli/package.json` - Metadata npm para @meacore/tauri-easy-updater-cli
- `crates/tauri-easy-updater/Cargo.toml` - Metadata para crates.io

### Documentación y licencias (creadas)
- `packages/core/README.md` y `LICENSE`
- `packages/cli/README.md` y `LICENSE`
- `crates/tauri-easy-updater/README.md` y `LICENSE`

## Requisitos para publicar

### 1. Configurar GitHub Secrets

Ir a: https://github.com/MeaCore-Enterprise/tauri-easy-updater/settings/secrets/actions

#### NPM_TOKEN (IMPORTANTE - Requiere configuración especial)

Si tienes 2FA habilitado en npm (recomendado), debes crear un token especial:

**Opción A: Granular Access Token (Recomendado)**
1. Ve a https://www.npmjs.com/settings/tokens
2. Click en "Generate New Token" > "Granular Access Token"
3. Configura:
   - **Name**: `github-actions-publish`
   - **Packages and scopes**: Selecciona "Read and write" para tus paquetes
     - `@meacore/tauri-easy-updater`
     - `@meacore/tauri-easy-updater-cli`
   - **Organizations**: No necesitas acceso a orgs
   - **⚠️ IMPORTANTE**: Marca "Bypass 2FA for this token"
4. Genera el token y cópialo

**Opción B: Classic Automation Token**
1. Ve a https://www.npmjs.com/settings/tokens
2. Click en "Generate New Token" > "Classic Token"
3. Selecciona tipo "Automation"
4. Genera el token

**Nota**: Si ves el error `403 Forbidden - Two-factor authentication or granular access token with bypass 2fa enabled is required`, significa que tu token no tiene el bypass 2FA habilitado.

#### CARGO_REGISTRY_TOKEN
1. Ve a https://crates.io/settings/tokens
2. Click en "New Token"
3. Selecciona scope: **publish-update**
4. Genera y copia el token

### 2. Ejecutar publicación

Opción A - Usar Windsurf:
```
/deploy
```

Opción B - Usar GitHub Actions:
1. Ir a https://github.com/MeaCore-Enterprise/tauri-easy-updater/actions/workflows/publish.yml
2. Click "Run workflow"
3. Seleccionar rama main
4. Ejecutar

### 3. Verificar publicación

```
/check-status
```

O manualmente:
```bash
npm view @meacore/tauri-easy-updater
npm view @meacore/tauri-easy-updater-cli
cargo search tauri-easy-updater
```

## Flujo de trabajo para futuros releases

1. Hacer cambios en el código
2. Ejecutar `/check-status` para ver versión actual
3. Actualizar versión en los package.json y Cargo.toml
4. Ejecutar `/release` para crear el release
5. Ejecutar `/deploy` para publicar
6. Verificar con `/check-status`

## Notas

- Los paquetes npm se publican como públicos (scope @meacore)
- El crate de Rust requiere estar en crates.io antes de que otros puedan usarlo
- Los workflows de GitHub Actions usan ubuntu-22.04 para compatibilidad con Tauri v1
