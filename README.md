# Órbita: quiz espacial

Aplicación web estática y autocontenida para poner a prueba tus conocimientos
sobre el espacio. Está implementada en un único archivo HTML, sin dependencias,
servidor ni proceso de compilación.

## Ejecutarla localmente

Abre `index.html` directamente en un navegador. En macOS también puedes usar:

```sh
open index.html
```

La aplicación incluye una pantalla inicial, preguntas con cuatro opciones,
feedback inmediato, barra de progreso, puntuación y una pantalla final con
opción para reiniciar el quiz.

## Publicación

El repositorio usa GitHub Actions para publicar el contenido estático en
GitHub Pages cada vez que se actualiza la rama `main`. El flujo de trabajo se
encuentra en `.github/workflows/deploy-pages.yml`.
