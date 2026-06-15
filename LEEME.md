# Pack Verano · Landing page

Landing page de venta del producto digital **Pack Verano** de Diletta Ghiglione (PDF de 38 páginas).
Página estática, sin backend: lista para subir a Vercel, Netlify o cualquier hosting.

## Archivos

- `index.html` : la landing page completa (todo en un único archivo).
- `gracias.html` : página de descarga a la que vuelve el cliente tras pagar.
- `assets/diletta.svg` : imagen de respaldo (se usa solo si no carga la foto real).
- `vercel.json` : configuración para desplegar en Vercel.

---

## 1. Poner el precio y activar el pago (lo único imprescindible)

Abre `index.html` y busca, casi al final, el bloque **CONFIG**:

```js
const CONFIG = {
  price:    "37€",
  priceOld: "49€",
  paypalLink: "",      // <- pega aquí tu enlace de PayPal
  stripeLink: "",      // <- opcional
  thankYouUrl: "gracias.html"
};
```

- `price` / `priceOld` : el precio se actualiza solo en toda la página.
- `paypalLink` : pega aquí tu enlace de cobro (ver punto 2).
- Mientras los enlaces estén vacíos, el botón mostrará un aviso recordándote que falta configurarlo.

---

## 2. Cobrar con PayPal (recomendado para empezar)

Tienes dos opciones, de la más simple a la más completa:

**Opción A. Botón "Comprar ahora" de PayPal (recomendada)**
1. Entra en PayPal Business → Herramientas → **Botones PayPal** → "Comprar ahora".
2. Pon el nombre ("Pack Verano"), el precio (37€) y, en las opciones avanzadas, la **URL de retorno** apuntando a tu `gracias.html` (ej. `https://tudominio.com/gracias.html`).
3. PayPal te da un enlace. Cópialo y pégalo en `paypalLink`.

**Opción B. Enlace PayPal.me (la más rápida, menos control)**
- Usa `https://www.paypal.com/paypalme/TUUSUARIO/37EUR` en `paypalLink`.
- Inconveniente: PayPal.me no redirige solo a la página de gracias, así que la entrega del PDF tendrás que hacerla por email (ver punto 4).

Con PayPal el cliente puede pagar con tarjeta como invitado, sin tener cuenta.

---

## 3. ¿Merece la pena añadir Stripe?

Para un PDF de 37€ vendido en España, **PayPal solo basta**. Stripe aporta valor si quieres:
- Apple Pay / Google Pay y una pantalla de pago más moderna.
- Comisiones algo más bajas.
- Redirección automática a `gracias.html` (Stripe Payment Links lo hace de serie).

Si lo activas: crea un **Payment Link** en Stripe, configura la URL de éxito a tu `gracias.html`, y pega el enlace en `stripeLink`. Si `stripeLink` tiene valor, se usa Stripe en lugar de PayPal.

> Atajo "todo en uno": si prefieres que el cobro **y** la entrega automática del PDF estén resueltos sin tocar nada, plataformas como **Gumroad** o **Payhip** suben el PDF, cobran con tarjeta/PayPal y lo entregan solas. En ese caso pondrías el enlace de Gumroad/Payhip en `paypalLink`.

---

## 4. Entregar el PDF

Ni PayPal ni Stripe envían el archivo por sí solos. Tres formas, de menos a más automática:

1. **Manual (para empezar)**: cuando te llegue el aviso de pago, respondes con el PDF adjunto por email. Cero configuración.
2. **Página de gracias**: sube el PDF junto a estos archivos (renómbralo `PACK-VERANO.pdf`) y en `gracias.html` el botón ya apunta a él. Configura la URL de retorno del pago a `gracias.html`.
3. **Automática total**: usa Gumroad/Payhip (punto 3), que envían el PDF solas tras el pago.

Recomendado: combinar 2 + un email automático de PayPal/Stripe con el enlace de descarga.

---

## 5. Publicar la página

**Vercel (gratis):** arrastra esta carpeta a vercel.com, o conéctala a un repositorio. Sin configuración extra.

**Subdominio sugerido:** `verano.dilettaghiglione.com` o una página dentro de su web.

---

## Notas de contenido

- Textos, precios, credenciales y reseñas tomados del PDF real y de dilettaghiglione.com.
- La foto del bloque "Sobre mí" se carga desde la web de Diletta; si algún día cambia, se mostrará la imagen de respaldo `assets/diletta.svg`.
- Precio actual de ejemplo: **37€** (tachado 49€). Cámbialo en CONFIG cuando lo decidáis.
