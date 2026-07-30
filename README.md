# perfil//sync

Plataforma de perfiles digitales públicos. Cada persona que entra crea su propio
perfil (`/p/sunombre`) gratis, lo personaliza desde su panel (`/editar`) y puede
conectarlo a Discord si quiere.

- 🧑 Tu perfil principal vive en `/p/ytk1` (Sinaloa, Minecraft, hacks, mods, redes).
- 🔐 Tu acceso al panel: usuario **ytk1** / contraseña **alexxx**
  (cambiable con la variable `PANEL_PASSWORD`).
- 🌎 Las páginas públicas no necesitan login: /, /p/sunombre, /crear.
- 📡 Discord es opcional: pegás un webhook en tu panel y solo se envía cuando
  vos apretás el botón (nada se manda automáticamente).

---

## Las líneas naranja que te salieron en Vercel **no son errores**

```
npm warn deprecated @esbuild-kit/esm-loader@2.6.5: Merged into tsx…
npm warn deprecated @esbuild-kit/core-utils@3.3.2: Merged into tsx…
```

Son avisos de dependencias viejas de **terceros** (no de tu código). Vercel las
ignora y sigue. El fallo real típico al desplegar una app con base de datos es
que:

1. No seteaste `DATABASE_URL` en Vercel, o
2. Las tablas no existen todavía.

Este proyecto se encarga del punto 2 **solo**: en el primer request crea las
tablas y siembra tu perfil `ytk1` automáticamente. Vos solo tenés que setear
`DATABASE_URL` en Vercel con una Postgres real.

---

## Cómo desplegar en Vercel en 5 pasos (gratis)

1. Subí este repo a GitHub.
2. En Vercel → New Project → importás el repo.
3. Antes de apretar **Deploy**, andá a **Environment Variables** y agregá:
   - `DATABASE_URL`: la URL de tu Postgres.
   - `PANEL_PASSWORD`: la contraseña que quieras para tu perfil (opcional, por defecto `alexxx`).
4. Obtener la Postgres gratis te lleva 1 click:
   - **Vercel Postgres** (Storage → Create Database) → copia `DATABASE_URL`
   - o **Neon**, **Supabase**, o **Railway**: todos dan una URL `postgresql://…`.
5. Apretá **Deploy**. La primera visita al sitio crea las tablas solas.

Si querés probar localmente:

```bash
cp .env.example .env.local
npm install
npm run dev
```

## Dominio propio tipo `ytk1.web`

El TLD `.web` puro no es gratuito. Las opciones reales y $0 son:

- `ytk1.vercel.app` (te lo da Vercel automático al desplegar).
- `ytk1.web.app` → creando un proyecto en Firebase Hosting y apuntándolo a tu
  deploy de Vercel.
- `ytk1.github.io` con GitHub Pages.

Si usas un dominio propio corto, solo agregá la variable
`DOMAIN_MAP='{"ytk1.web.app":"ytk1"}'` en Vercel y la portada mostrará tu perfil
cuando entren por ese dominio.

## Comandos útiles

- `npm run dev` → servidor de desarrollo
- `npm run build` → build de producción
- `npm run start` → correr el build
- `npm run typecheck` → revisar tipos
- `npm run db:push` → forzar el schema desde Drizzle (opcional)
