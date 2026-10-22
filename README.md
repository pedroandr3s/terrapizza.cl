# Terra Pizza — catálogo web

Catálogo de Terra Pizza (San Carlos, Ñuble) con intro animada y pedidos de varias pizzas por WhatsApp. Es HTML, CSS y JavaScript sin frameworks ni dependencias.

## Levantar en localhost

Requiere Node 18 o superior.

```bash
npm start
```

Abre http://localhost:5173

Para usar otro puerto en PowerShell: `$env:PORT=3000; npm start`

Alternativas sin Node: `python -m http.server 5173` o `npx serve .` dentro de esta carpeta.

## Estructura

```
terra-pizza/
├── index.html              Página completa (estilos y script incluidos)
├── scripts/dev-server.js   Servidor local sin dependencias (sirve public/)
├── assets/                 Logo, favicon y recortes de la mascota
│   ├── mascota-scooter.webp   Mascota en scooter (intro)
│   ├── mascota-caja.webp      Frente de la caja: tapa las pizzas al entrar a la mochila
│   └── mascota-saludo.webp    Mascota saludando (carta)
├── frames/                 Aquí van los frames del video de Gemini (16:9)
├── frames-vertical/        Frames opcionales 9:16 para celulares
└── referencias-gemini/     Imágenes de partida para generar el video
```

## Dónde se edita cada cosa (en index.html)

- **Pizzas, precios e ilustraciones:** el arreglo `PIZZAS` en el script y los `<li class="item">` de la carta. Si cambias un precio, cámbialo en ambos lugares.
- **Número de WhatsApp:** la constante `WA` (y los enlaces `wa.me` del HTML).
- **Costo de delivery:** la constante `DELIVERY`.
- **Horario y estado abierto/cerrado:** la función `updateStatus` y la tabla `.hours`.
- **Colores y tipografías:** las variables en `:root`.

## La intro

- Se muestra una vez por sesión. Para verla de nuevo, abre la página en una pestaña nueva o ejecuta `sessionStorage.removeItem('terra-intro')` en la consola.
- No aparece si el sistema tiene activado "reducir movimiento".
- Tiene botón "Saltar intro" y también se salta con Esc.

### Activar el video de Gemini

1. Exporta el video como frames WebP numerados: `frames/terra_0001.webp`, `terra_0002.webp`, …
2. En `index.html`, en la constante `SEQ`, cambia `frames: 0` por el total de frames.
3. Opcional: lo mismo con la versión vertical en `frames-vertical/` y `SEQ.vertical.frames`.

Mientras `frames` sea 0, la intro usa la animación ilustrada.

## Pedidos

El pedido se guarda en el navegador del cliente (`localStorage`, clave `terra-pedido`) y se envía como mensaje de texto al WhatsApp del local. No hay pagos ni servidor de pedidos.
