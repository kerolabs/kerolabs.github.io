# kerolabs.github.io

Páginas públicas de los enlaces que comparte Pozzo, la app para administrar juntas del equipo Kerolabs (UPC). La landing del producto está en [pozzo-landing-page](https://github.com/kerolabs/pozzo-landing-page).

## Qué incluye

| Ruta | Para qué sirve |
|---|---|
| `unirme/?c=JB7K4M` | Invitación a una junta: muestra el código y cómo unirse desde la app. |
| `historial/?t=<token>` | Historial compartido: resumen de puntualidad de un miembro, leído del backend. |
| `404.html` | Página para enlaces que no existen. |
| `index.html` | Redirige a la landing. |

El backend arma estos enlaces con `INVITATIONS_LINK_BASE_URL` y `COMPLIANCE_SHARED_LINK_BASE_URL`. La página del historial consulta `GET /api/v1/compliance/shared/{token}` en `api-kerolabs.duckdns.org`, que es público.

Es un sitio estático, sin build ni dependencias. `.nojekyll` evita que GitHub Pages ignore las carpetas que empiezan con punto, como `.well-known/`, donde irá el `assetlinks.json` de los App Links de Android.

## Cómo verlo en local

```
python -m http.server 8000
```

Luego abre `http://localhost:8000/unirme/?c=JB7K4M`.

## Cómo contribuir

`main` publica el sitio y `develop` integra el trabajo. Ninguna de las dos acepta push directo: los cambios entran por pull request y el check `commit-policy` exige [Conventional Commits](https://www.conventionalcommits.org/) en inglés. El hook `.githooks/commit-msg` aplica la misma regla antes de crear el commit; como el sitio no tiene paso de compilación, actívalo una vez después de clonar:

```bash
git config core.hooksPath .githooks
```
