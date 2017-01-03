# Html y Sass
Para crear html primero hay que pensar o apostar porque mas adelante se pueda crear una guía de estilo ya que nos ayudará a **estandarizar nuestro código** y asi cuando alguien nuevo se una al equipo de desarrollo, pueda leer la guía de estilo creada y seguir las mismas **prácticas de desarrollo**.

### Html: etiquetas globales
Sabiendo que el nuevo proyecto se diseño correctamente y comensaremos por estilizar nuestras etiquetas html globales como h1, h2, p, ul ,etc; como tamaños, colores, entre otras.

### Escribir html
Aspectos importantes a tomar en cuenta antes de empezar a crear nuestro html:
* Crear html para reutilizar: Componentes con clases, ejm: button, tags, cards, etc .
* Pensar que el SEO de una web puede cambiar pero no el UI ni el UX - Evita estilizar a las etiquetas html directamente(h1, h2, h3, div, article, etc) en su lugar crea clases.
* Escribe tus clases del html con un nombre general(la finalidad es usar los componentes en diferentes páginas e incluso otro proyecto) e intenta escribirlas a lo más que puedas en inglés(botones: `.btn`).
* Usa las etiquetas html de [forma correcta](https://github.com/jonmircha/buenas-practicas-frontend/blob/master/teoria-html.md).

### Escribir Sass
Consideraciones básicas:
* Define variables para colores, fuentes, tamaños, etc. que vas a usar con frecuencia.
* Anidamiento Máximo: 3 niveles, o si lo usas puede ser para un extend de algo puntual.
* Pensar siempre en responsive teniendo en cuenta el enfoque **First Mobile**.
* Pensar en responsive no significa desktop y mobile, significa que el contenido responsive q vayamos a crear debe verse bién desde la medida básica de mobile(ref:320px) hasta la medida mas alta de una desktop(UHD:1920px | Estandar: 1366px).
* Nunca uses el selector #id para estilizar, salvo caso muy especial.
* Empieza por crear pequeños componentes que puedas reutilizar en cualquier parte de tu proyecto e incluso en otro.
* Prepara tus componentes para aceptar variaciones ya sea de tamaños o de color.
* Evita usar !important salvo caso especial.
* Si usas un framework evita sobreescribir sus clases mas bién extiende si los vas a usar.

#### Ejemplo básico de uso
* **Emmet html:**
`.card.card-primary>(.card__head>h3.card__title)+.card__body+.card__footer`.
* **Sass input:**
```sass
/* card.scss */
.card {
    &-primary { }
    &__head { }
    &__title { }
    &__body { }
}
```
* **Css output:**
```css
.card { }
.card-primary { }
.card__head { }
.card__title { }
.card__body { }
```
* `.card` es el “bloque” y representa el componente de más alto nivel.
* `.card__head`, `.card__title` son  “elementos” y representan un descendiente de `.card` que ayuda a componer el bloque en su conjunto.
* `.card-primary` es un “modificador” y representa un estado diferente o variación del bloque `.card`.

#### Ejemplo de uso html:pug

```pug
header
  h1.text-center Nuestro Blog 
br 

div.container
  div.row
    div.col.xs-12.sm-6
      article.post
        div.post__head
           h3.post__title Título del post
           span.post__count.badge.badge-line 100
        div.post__body
          p Contenido del card  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ex at, sint officia, assumenda atque ducimus possimus.
        div.tags.post__tags
          a(href="#") html
          a(href="#") css
          a(href="#") sass
        div.post__footer
          small By 
            a(href="#") @kenyk7
          a(href="#").btn.btn-sm.post__learn-more Ver más
    div.col.xs-12.sm-6
      article.post.post-primary
        div.post__head
           h3.post__title Título del post
           span.post__count.badge.badge-line 100
        div.post__body
          p Contenido del card  Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ex at, sint officia, assumenda atque ducimus possimus.
        div.tags.post__tags
          a(href="#") html
          a(href="#") css
          a(href="#") sass
        div.post__footer
          small By 
            a(href="#") @kenyk7
          a(href="#").btn.btn-primary.btn-sm.post__learn-more Ver más

br
p.text-center
   a(href="#").btn Cargar más

br
.container
  <script src="https://gist.github.com/kenyk7/1f9c3a8fd9804f223376a2637fd81979.js"></script>
```

#### Ejemplo de uso sass

```scss
// Variables
//----------------------
$brand-primary: #3498db;
$brand-second: #222;
$grid-size: 20px;

// Globals
//----------------------
* {
  box-sizing: border-box;
}
body {
  font-size: 16px;
  overflow-x: hidden;
  // demo
  padding-left: 10px;
  padding-right: 10px;
}

// Grilla
//----------------------
.container {
  width: 100%;
  max-width: 960px;
  margin: 0 auto;
  padding-left: $grid-size/2; 
  padding-right: $grid-size/2;
}
.row {
  margin-left: -$grid-size/2;
  margin-right: -$grid-size/2;
  &:after {
    content: "";
    display: table;
    clear: both;
  }
}
.col {
  padding-left: $grid-size/2;
  padding-right: $grid-size/2;
  position: relative;
  float: left;
}
.xs-12 {
  width: 100%;
}
//Enfoque first mobile
@media (min-width: 480px){
  .sm-6 {
    width: 50%;
  }
}

// Helpers
//----------------------
.pull-right {
  float: right !important;
}
.text-center {
  text-align: center;
}
.text-right {
  text-align: right;
}
.clearfix {
  clear: both;
}

// Components
//----------------------

// Btns
.btn {
  background: $brand-second;
  color: #fff;
  padding: 10px 15px;
  border-radius: 2px;
  text-decoration: none;
  // btn variation
  &-primary {
    background: $brand-primary;
    color: #fff;
  }
  // btn sizes
  &-sm {
    font-size: 14px;
    padding: 5px 10px;
  }
}

// Tags
.tags {
  a {
    display: inline-block;
    text-decoration: none;
    margin: 0 3px;
    padding: 3px 5px;
    border-radius: 3px;
    background: #ccc;
    color: #000;
  }
}

// Badges
.badge {
  font-size: 12px;
  padding: 3px 7px;
  border-radius: 10px;
  background: #555;
  border: 1px solid #555;
  // badge variation
  &-line {
    background: none;
    border: 1px solid #fff;
  }
}

// Post component
//----------------------
.post {
  margin-bottom: 15px;
  box-shadow: 0 1px 3px rgba(#000, 0.2);
  // Post variations
  &-primary {
    .post__head {
      background: $brand-primary;
    }
  }
  &__head {
    background: $brand-second;
    color: #fff;
    padding: 15px;
    position: relative;
  }
  &__title {
    font-size: 20px;
    font-weight: 300;
    margin: 0;
    margin-right: 40px;
  }
  &__count {
    position: absolute;
    right: 15px;
    top: 50%;
    transform: translateY(-50%);
  }
  &__body {
    padding: 10px 15px;
  }
  &__tags {
    border-top: 1px solid #f5f5f5;
    padding: 7px 15px;
    background: #f9f9f9;
    a {
      font-size: 12px;
    }
  }
  &__footer {
    padding: 15px;
    background: #f0f0f0;
    small {
      a {
        color: #000;
      }
    }
    .post__learn-more {
      float: right;
      margin-top: -4px;
    }
  }
}

```

#### Preview en Codepen
http://codepen.io/kenyk7/pen/RoQrOE

### Referencias para más información
* [Guía de Estilo CSS / Sass de Airbnb](https://github.com/ismamz/guia-de-estilo-css)
* [Buenas practicas frontend](https://github.com/jonmircha/buenas-practicas-frontend)
* [Cssreference.io](http://cssreference.io/)

License
----

MIT
