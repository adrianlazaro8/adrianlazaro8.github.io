+++
date = '2025-09-05T18:41:00+01:00'
draft = false
title = 'Ofusca El Codigo De Tu Aplicación Android'
description = "Conoce cómo ofuscar el código de tu aplicación Android para que a nadie le sirva hacer ingeniería inversa"

# LoveIt configuration
featuredImage = "/images/ofusca_el_codigo_de_tu_aplicacion_android.png"
featuredImagePreview = "/images/ofusca_el_codigo_de_tu_aplicacion_android.png"
tags = ["Seguridad"]
+++

Entramos a ver un tema que sobre todo al principio de nuestra vida profesional como desarrolladores Android no cuidamos lo suficiente (principalmente por desconocer la existencia de este tipo de herramientas). **Ofusca el código fuente de tu aplicación** si quieres evitar a toda costa sorpresas desagradables.

Si quieres más definiciones para poder seguir haciéndote una idea, te dejo por aquí la de la [RAE](https://dle.rae.es/ofuscar "Definición de ofuscar en la RAE").

---

### Objetivos principales de la ofuscación:
* **Dificultar la ingeniería inversa:** Impedir que otros entiendan cómo funciona tu algoritmo.
* **Seguridad por oscuridad:** Aunque no es una medida de seguridad definitiva, dificulta la búsqueda de brechas.
* **Reducción de tamaño:** A menudo, el proceso de ofuscación elimina espacios y renombra variables a una sola letra, lo que reduce el peso del archivo (minificación).

---

## Técnicas comunes de ofuscación

Para lograr que el código sea ininteligible, las herramientas suelen aplicar varias capas de transformación:

1.  **Renombrado de variables y funciones:** Cambiar `calcularSalario()` por `a()`.
2.  **Alteración del flujo de control:** Reorganizar bucles y condicionales para que el camino lógico no sea lineal.
3.  **Codificación de strings:** Convertir textos planos en hexadecimal o Base64 para que no se puedan buscar palabras clave en el binario.
4.  **Inserción de código muerto:** Añadir código que no hace nada para confundir al analista.

---

## Ejemplo práctico con Kotlin

Imagínate que has implementado una funcionalidad relativamente sensible en tu aplicación Android (vamos a suponer que no existe el backend). Esta funcionalidad se habilita o se deja deshabilitada en base a si el usuario ha hecho una compra in-app determinada.

Dicha comprobación no es descabellado pensar que se hace a través de un if else o de alguna forma muy similar. Imagínate, también, que alguien tiene acceso al código fuente de tu app y lo puede modificar a su antojo… ¿Qué crees que podría pasar? ¡BINGO!

```kotlin
if(user.isSubscribed()){
  //Very cool functionality
} else {
  //Show purchase dialog
}
```

Efectivamente, podrían modificar ese if else para que la aplicación se comporte tal y como ellos esperan, porque todo lo que tú habías implementado lo pueden leer y llegar a entender de forma bastante sencilla.

Aquí entra en juego la ofuscación. La ofuscación del código fuente es ese proceso que se encarga de modificar el nombre de las clases, de las variables, de las constantes, etc… Con ello, si alguien decompila un APK no podrá llegar a entender qué está haciendo una parte del código. En lugar de el snippet de arriba, podría llegar a encontrar algo como esto:

```kotlin
if(a.e()){
  //Very cool functionality
} else {
  //Show purchase dialog
}
```

A la persona que está indagando en cosas que no debería, a priori, no se le va a pasar por la cabeza que modificando ese if else consiga acceso a esa funcionalidad tan chula sin pagar 💪. ¡Le acabamos de poner una barrera muy importante!

### Muy bien, muy bien… ¿Pero cómo hago yo eso?

Existen varias alternativas, pero de las más conocidas son:

- ProGuard: Herramienta de software libre, y que está muy integrada con Android Studio. Más información: https://developer.android.com/studio/build/shrink-code?hl=es
- DexGuard: Es una herramienta comercial derivada de ProGuard, con más potencia a la hora de ofuscar. Más información: https://www.guardsquare.com/dexguard

En un próximo artículo explicaremos cómo utilizar ProGuard, pero independientemente de la herramienta a utilizar, insisto, debes recordar que es muy importante ofuscar tu código fuente antes de subirlo a la tienda.

¡Nos leemos en próximos artículos! Disfruta de la semana y recuerda que siempre puedes revisar cuando quieras el resto de artículos 🤗

