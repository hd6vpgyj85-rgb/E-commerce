# Yukly Store

Tienda de peluches y coleccionables 100% gratuita: sin servidor propio y sin pasarela de pagos. Los pedidos se cierran por WhatsApp.

## Archivos

- `index.html` — tienda pública (catálogo, carrito, checkout por WhatsApp).
- `admin-login.html` — login del panel administrativo.
- `admin.html` — panel administrativo (productos y colecciones), protegido por Firebase Authentication.
- `firestore.rules` — reglas de seguridad de Firestore.

## Configuración

1. Crea un proyecto en [Firebase Console](https://console.firebase.google.com).
2. Activa **Firestore Database** (modo producción) y **Authentication** con el proveedor **Email/contraseña**.
3. Crea un usuario administrador en Authentication → Users.
4. Publica las reglas de `firestore.rules` en Firestore → Reglas.
5. En Firestore, crea las colecciones `collections` y `products` (pueden iniciar vacías; se administran desde el panel).
6. Copia la configuración web de tu proyecto (Configuración del proyecto → Tus apps → SDK setup) y reemplaza el bloque `firebaseConfig` en `index.html`, `admin-login.html` y `admin.html`:

```js
const firebaseConfig = {
  apiKey: "TU_API_KEY",
  authDomain: "TU_AUTH_DOMAIN",
  projectId: "TU_PROJECT_ID",
  storageBucket: "TU_STORAGE_BUCKET",
  messagingSenderId: "TU_MESSAGING_SENDER_ID",
  appId: "TU_APP_ID"
};
```

7. Publica el repositorio en **GitHub Pages** (Settings → Pages → rama y carpeta raíz).

## Modelo de datos

**collections**: `name` (string), `description` (string), `image` (string URL), `createdAt` (timestamp).

**products**: `name` (string), `price` (number), `stock` (number), `collectionId` (string, FK a collections), `brand` (string), `tags` (array de strings), `description` (string), `image` (string URL), `createdAt` (timestamp).

## Pedidos

Los clientes arman su carrito en la tienda y al finalizar se genera un mensaje prellenado que se envía por WhatsApp al +52 656 8596503.
