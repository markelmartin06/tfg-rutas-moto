# Cómo contribuir a tfg-rutas-moto

Esta guía explica el flujo de trabajo con ramas y pull requests del proyecto. Se aplica a cualquier persona o IA que haga cambios en el repositorio.

## Ramas principales

| Rama      | Para qué sirve                                                    | Quién mergea en ella |
|-----------|-------------------------------------------------------------------|----------------------|
| `main`    | Producción. Solo contiene código probado en `staging`.            | Markel (revisor/administrador) |
| `staging` | Preproducción. Aquí se prueba un grupo de tareas antes de publicar. | Markel |
| `develop` | Integración. Aquí llegan todas las tareas terminadas.             | Markel |

Nadie hace commits directos en `main`, `staging` ni `develop`. Todo cambio entra mediante un pull request.

## Ramas de trabajo

Cada tarea o hotfix se hace en **su propia rama**, creada a partir de `develop` y actualizada con `git pull`:

```bash
git switch develop
git pull
git switch -c feature/registro-de-usuarios
```

El nombre de la rama tiene dos partes:

1. **Prefijo** que dice qué tipo de rama es:
   - `feature/` para una tarea nueva o una mejora.
   - `hotfix/` para corregir un error.
2. **Descripción breve** de lo que hace la rama, en minúsculas, en español y con palabras separadas por guiones.

Ejemplos:

- `feature/mapa-de-rutas-con-leaflet`
- `feature/subir-ruta-desde-gpx`
- `hotfix/login-falla-con-mayusculas`

Una rama = una tarea. Si aparece algo distinto, se abre otra rama.

## Pull requests

1. Cuando la rama esté terminada y probada, se abre un PR **hacia `develop`**. Nunca hacia `staging` ni hacia `main`.
2. El único que puede aprobar y mergear el PR es el revisor/administrador (Markel).
3. El título del PR resume el cambio, y la descripción explica qué se ha hecho y cómo probarlo.

## Paso a staging y a producción

1. Cuando un grupo de tareas de `develop` funciona bien en conjunto, Markel abre un PR **de `develop` a `staging`**, lo revisa y, si todo está correcto, lo mergea.
2. Cuando todo funciona correctamente en `staging`, se hace un PR **de `staging` a `main`** y se pasa a producción.

```
feature/... ─┐
hotfix/...  ─┼─► develop ──► staging ──► main
feature/... ─┘   (PR)        (PR)        (PR)
```

## Resumen rápido

- Crea la rama desde `develop` con el prefijo `feature/` o `hotfix/`.
- Abre el PR solo hacia `develop`.
- Solo Markel aprueba y mergea.
- `develop` pasa a `staging` y `staging` pasa a `main`, siempre mediante un PR revisado por Markel.
