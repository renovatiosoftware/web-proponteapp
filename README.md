# web-proponteapp — Sitio estático (GitHub Pages) para proponteapp.com

Sirve la **Política de Tratamiento de Datos** de ProPonte en una URL pública, requisito de
Google Play (Data Safety) y de la Ley 1581/2012. Sitio estático, sin build.

## Estructura
- `index.html` — holding page de ProPonte (raíz del dominio).
- `politica/index.html` — la política → **URL a declarar: `https://proponteapp.com/politica/`**.
- `CNAME` — dominio personalizado (`proponteapp.com`) para GitHub Pages.
- `.nojekyll` — evita el procesamiento Jekyll (servimos HTML tal cual).

## Publicar en GitHub Pages (una vez)
1. Crea un repo en GitHub, p. ej. **`web-proponteapp`** (público; Pages gratis requiere repo público en cuentas free).
2. Sube el **contenido de esta carpeta** a la raíz del repo (rama `main`):
   ```bash
   cd "web-proponteapp"
   git init && git add . && git commit -m "Sitio proponteapp.com + política"
   git branch -M main
   git remote add origin https://github.com/<tu-usuario>/web-proponteapp.git
   git push -u origin main
   ```
3. En GitHub → **Settings → Pages** → *Source*: `Deploy from a branch` → rama `main`, carpeta `/ (root)`.
4. En **Settings → Pages → Custom domain** escribe `proponteapp.com` y guarda. Marca **Enforce HTTPS**
   (puede tardar minutos en habilitarse mientras emite el certificado).

## DNS en tu registrador (donde compraste proponteapp.com)
Apunta el dominio APEX a las IP de GitHub Pages (registros **A**):
```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```
Opcional IPv6 (registros **AAAA**): `2606:50c0:8000::153`, `...8001::153`, `...8002::153`, `...8003::153`.
Y el subdominio **www** como CNAME a tu usuario:
```
CNAME   www   <tu-usuario>.github.io.
```
La propagación DNS puede tardar de minutos a ~24 h.

## Verificar
- `https://proponteapp.com/` → holding page.
- `https://proponteapp.com/politica/` → política (esta es la URL para Play Console y `Responsable.URL_POLITICA`).

## Actualizar la política
Edita `politica/index.html` (fuente de referencia: `android-proponte/docs/legal/politica-privacidad.md`)
y vuelve a hacer `git push`. Pages redepliega solo.
