<h1 id='summary'>Summary</h1>

-   [CSS](#css)
    -   [Basics](#cssbasics)
        -   [Reset Project](#resetproject)
        -   [Body Element](#body)
        -   [Adding Background Image](#addingbgimage)
        -   [Positioning](#positioning)
            -   [Centering Element](#centeringelement)
        -   [Span Element](#spanelement)
        -   [Converting Pixel to REM](#convertingpxtorem)
        -   [Good Practice - Reseting the Project](#goodpractice)
    -   [Animation](#animation)
        -   [@keyframes](#keyframes)
        -   [Transition](#transition)
-   [BEM (Block Element Modifier) Methodology](#bem)
-   [Sass](#sass)
    -   [Sass Variables and Nesting](#sassvariables)
    -   [Sass Mixin](#sassmixin)
    -   [Sass Functions](#sassfunctions)
    -   [Sass Extend](#sassextend)
    -   [Sass Partials](#sasspartials)
        -   [Import Partials](#sassimportpartial)

<h1 id='css'>CSS</h1>

<h2 id='cssbasics'>Basics</h2>

<h3 id='resetproject'>Reset Project</h3>

[Go Back to Summary](#summary)

-   Before start styling our website, a good practice is to reset all the browser parameters. Each browser has different parameters and we want to display our website the same way in all browsers.

    -   the `box-sizing: border-box;` removes the box margin and padding to not be considered in the total width or total height of the element

    ```CSS
      * {
          margin: 0;
          padding: 0;
          box-sizing: border-box;
      }
    ```

<h3 id='body'>Body Element</h3>

[Go Back to Summary](#summary)

-   A good practice is to define the `font-family` in the body element, instead of the generic `*`

    ```CSS
      body {
          font-family: 'Lato', sans-serif;
          font-weight: 400;
          font-size: 16px;
          //- 1.7 times bigger than the font height
          line-height: 1.7;
          color: #777;
          padding: 30px;
      }
    ```

<h3 id='addingbgimage'>Adding Background Image</h3>

[Go Back to Summary](#summary)

-   To an image as a background we simply call `background-image: url(<relative_path/image>)`

    -   With `background-image` we also can specify the gradient property
    -   Before the `url()` we can specify `linear-gradient(direction, from-color, to-color)`
        -   Ideally we specify the color as `rgba` so we we can set the **opacity**
        -   We can specify more than one direction, such as `to right bottom`
    -   `background-size: cover;` tries to fit the image inside the box to use the whole available width. If we change the **viewport** the image will be resized until the height hits e available height of the element
    -   `background-position: top;` ensures that the top of the image is always visible, and the bottom is cropped if bigger the than the available space
    -   `clip-path: polygon(x y, x y, x y, x y)` displays only the defined area of the image
        -   [clip-path maker - Website](https://bennettfeely.com/clippy/)

<h3 id='positioning'>Positioning</h3>

[Go Back to Summary](#summary)

-   **Static**
    -   HTML elements are positioned static by default.
    -   Static positioned elements are not affected by the top, bottom, left, and right properties.
    -   An element with `position: static;` is not positioned in any special way; it is always positioned according to the normal flow of the page
-   **Relative**
    -   An element with `position: relative;` is positioned relative to its normal position.
    -   Setting the `top`, `right`, `bottom`, and `left` properties of a relatively-positioned element will cause it to be adjusted away from its normal position. Other content will not be adjusted to fit into any gap left by the element.
-   **Absolute**
    -   An element with `position: absolute;` **is positioned relative to the nearest positioned ancestor** (instead of positioned relative to the viewport, like fixed).
    -   However; if an absolute positioned element has no positioned ancestors, it uses the document body, and moves along with page scrolling.
    -   **Note:** A "positioned" element is one whose position is anything except static.
-   **Fixed**

    -   An element with `position: fixed;` **is positioned relative to the viewport**, which means it always stays in the same place even if the page is scrolled. The top, right, bottom, and left properties are used to position the element.
    -   A fixed element does not leave a gap in the page where it would normally have been located.
    -   **Notice the fixed element in the lower-right corner of the page.**

    ```SCSS
      .header {
          height: 95vh;
          background-image: linear-gradient(
                  to right bottom,
                  rgba(126, 213, 111, 0.8),
                  rgba(40, 180, 131, 0.8)
              ),
              url('../img/hero.jpg');
          background-size: cover;
          background-position: top;
          clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
          position: relative;

          &__logo-box {
              position: absolute;
              top: 40px;
              left: 40px;
              &__logo {
                  height: 35px;
              }
          }
      }
    ```

<h4 id='centeringelement'>Centering Element</h4>

-   To center an element in the middle of the screen, one option is to use the **absolute** position
-

<h3 id='spanelement'>Span Element</h3>

[Go Back to Summary](#summary)

-   `<Span>` element by default is `inline` element, just like text
-   If we change to **display** property to **block**, the the span will use ahh the available width
-   We then can define a `.text-box` to set the position as **absolute** and the parent element (`header`) as **relative**

    -   with that set, we can define the `top` and `left` position
        -   That's now enough to centralize the `.text-box`, we need to a `transform`
        -   `transform: translate(-50%, -50%)` to shift the component position

    ```SCSS
      .header {
          height: 95vh;
          background-image: linear-gradient(
                  to right bottom,
                  rgba(126, 213, 111, 0.8),
                  rgba(40, 180, 131, 0.8)
              ),
              url('../img/hero.jpg');
          background-size: cover;
          background-position: top;
          clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
          position: relative;

          &__text-box {
              position: absolute;
              top: 40%;
              left: 50%;
              transform: translate(-50%, -50%);
              text-align: center;
              &__heading-primary {
                  color: white;
                  text-transform: uppercase;
                  margin-bottom: 60px;

                  backface-visibility: hidden;
                  &__main {
                      display: block;
                      font-size: 60px;
                      font-weight: 400;
                      letter-spacing: 35px;

                      animation-name: moveInLeft;
                      animation-duration: 1s;
                      animation-timing-function: ease-in-out;
                  }
                  &__sub {
                      display: block;
                      font-size: 20px;
                      font-weight: 700;
                      letter-spacing: 17.4px;

                      animation: moveInRight 1s ease-in-out;
                  }
              }
          }
      }
    ```

<h3 id='convertingpxtorem'>Converting Pixel to REM</h3>

[Go Back to Summary](#summary)

-   If we have set our `html` to `font-size: 16px` this means that `1rem` is equal to `16px`
-   So we can convert `rem` using the **rule of three**

    |  px  |    rem     |
    | :--: | :--------: |
    | 15px | 0.9375 rem |
    | 16px |   1 rem    |
    | 17px | 1.0625 rem |

<h3 id='goodpractice'>Good Practice - Reseting the Project</h3>

[Go Back to Summary](#summary)

-   a good practice instead of just selecting the all elements (`*`), we can select the `::before` and `::after` pseudo elements, and define the reset parameters

    ```SCSS
      *,
      *::before,
      *::after {
          margin: 0;
          padding: 0;
          box-sizing: inherit;
      }
    ```

    -   and then inside of the `body` element, we define the `box-sizing` to `border-box`

    ```SCSS
      body {
          font-family: 'Lato', sans-serif;
          font-weight: 400;
          font-size: 0.16rem;
          line-height: 1.7;
          color: #777;
          padding: 3rem;

          //- the `box-sizing: border-box;` removes the box margin and padding to not be considered in the total width or total height of the element
          box-sizing: border-box;
      }
    ```

-   another good practice is to define the default `font-size` of the project

    -   To do so, we define in the `html` tag, and we set to `10px` so we can easily convert into REM

    ```SCSS
      html {
          font-size: 10px;
      }
    ```

    -   We could also use in **%**, we just have to convert the `10px`.
    -   By default the `font-size` is `16px`, so we just need to divide `10px/16px = 0.625` or `62.5%`

    ```SCSS
      html {
          font-size: 62.5%;
      }
    ```

<h2 id='animation'>Animation</h2>

<h3 id='keyframes'>@keyframes</h3>

[Go Back to Summary](#summary)

-   To use `@keyframes` we need to give a name to the animation
-   Then we define:

    -   `0%` before the animation starts
    -   `80%` middle of the animation
    -   `100%` when the animation finishes

    ```SCSS
      @keyframes moveInLeft {
          0% {
              opacity: 0;
              transform: translateX(-100px);
          }

          80% {
              transform: translateX(10px);
          }

          100% {
              opacity: 1;
              transform: translate(0p);
          }
      }
    ```

-   Then to use, we need to define:

    -   `animation-name`
    -   `animation-duration`
    -   `animation-timing-function`
    -   `animation-fill-mode: backwards;` - applies the animation styles to the element before starting the animation (this is necessary, when the page loads)
    -   `animation-delay` - adds a delay before starting the animation

    ```SCSS
      &__heading-primary {
          color: white;
          text-transform: uppercase;
          margin-bottom: 60px;
          backface-visibility: hidden;
          &__main {
              display: block;
              font-size: 60px;
              font-weight: 400;
              letter-spacing: 35px;

              animation-name: moveInLeft;
              animation-duration: 1s;
              animation-timing-function: ease-in-out;
              animation-delay: 0.75s;
              // animation-iteration-count: 3;
          }
      }
    ```

-   A shorthand version:

    -   `animation: moveInLeft is ease-in-out 0.75s;`

-   Fixing animations alignment
    -   Sometimes the **transform** property can gets bugged and the animation doesn't work properly
    -   An easy fix is to define `backface-visibility: hidden;` to the closest parent element

<h3 id='transition'>Transition</h3>

[Go Back to Summary](#summary)

-   An easy way to work with animation we can use the `transition` property, where we to:
    -   Defined the initial state of the element
        -   `transition: all 0.2s;`, in this case we are enabling the transition to this element with **all** transitions available and with a duration of `0.2s` (**this is the initial state**)
    -   Then to execute the animation, we just need do define the type of the transition
        -   `transform: translateY(-3px);`, in this case we are changing the position **3 pixels up**
-   with the help of **pseudo classes** and **pseudo elements**, we can add more styling to our elements

    ```SCSS
      &__btn {
          text-transform: uppercase;
          text-decoration: none;
          display: inline-block;
          border-radius: 100px;
          transition: all 0.2s;
          position: relative;
          animation: moveInBottom 0.5s ease-out 0.75s;
          animation-fill-mode: backwards;

          &--white {
              @extend .header__text-box__btn;
              background-color: white;
              color: #777;
              padding: 15px 40px;
              &::after {
                  background-color: white;
              }
          }
          &:hover {
              transform: translateY(-3px);
              box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
              &::after {
                  transform: scaleX(1.4) scaleY(1.6);
                  opacity: 0;
              }
          }
          &:active {
              transform: translateY(-1px);
              box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
          }
          &::after {
              content: '';
              display: inline-block;
              height: 100%;
              width: 100%;
              border-radius: 100px;
              position: absolute;
              top: 0;
              left: 0;
              z-index: -1;
              transition: all 0.4s;
          }
      }
    ```

-   in this case we used `:hover` and added a `transform: translateY(-3px);` to do simply animation to move the button up
-   and once it clicked `:active`, we animate again to `transform: translateY(-1px);`

-   **All CSS Pseudo Classes**
    | Selector | Example | Example description |
    | ------------------------- | -------------------------- | -------------------------------------------------------------------------------------------------------- |
    | :active | a:active | Selects the active link |
    | :checked | input:checked | Selects every checked `<input>` element |
    | :disabled | input:disabled | Selects every disabled `<input>` element |
    | :empty | p:empty | Selects every `<p>` element that has no children |
    | :enabled | input:enabled | Selects every enabled `<input>` element |
    | :first\-child | p:first\-child | Selects every `<p>` elements that is the first child of its parent |
    | :first\-of\-type | p:first\-of\-type | Selects every `<p>` element that is the first `<p>` element of its parent |
    | :focus | input:focus | Selects the `<input>` element that has focus |
    | :hover | a:hover | Selects links on mouse over |
    | :in\-range | input:in\-range | Selects `<input>` elements with a value within a specified range |
    | :invalid | input:invalid | Selects all `<input>` elements with an invalid value |
    | :lang\(language\) | p:lang\(it\) | Selects every `<p>` element with a lang attribute value starting with "it" |
    | :last\-child | p:last\-child | Selects every `<p>` elements that is the last child of its parent |
    | :last\-of\-type | p:last\-of\-type | Selects every `<p>` element that is the last `<p>` element of its parent |
    | :link | a:link | Selects all unvisited links |
    | :not\(selector\) | :not\(p\) | Selects every element that is not a `<p>` element |
    | :nth\-child\(n\) | p:nth\-child\(2\) | Selects every `<p>` element that is the second child of its parent |
    | :nth\-last\-child\(n\) | p:nth\-last\-child\(2\) | Selects every `<p>` element that is the second child of its parent, counting from the last child |
    | :nth\-last\-of\-type\(n\) | p:nth\-last\-of\-type\(2\) | Selects every `<p>` element that is the second `<p>` element of its parent, counting from the last child |
    | :nth\-of\-type\(n\) | p:nth\-of\-type\(2\) | Selects every `<p>` element that is the second `<p>` element of its parent |
    | :only\-of\-type | p:only\-of\-type | Selects every `<p>` element that is the only `<p>` element of its parent |
    | :only\-child | p:only\-child | Selects every `<p>` element that is the only child of its parent |
    | :optional | input:optional | Selects `<input>` elements with no "required" attribute |
    | :out\-of\-range | input:out\-of\-range | Selects `<input>` elements with a value outside a specified range |
    | :read\-only | input:read\-only | Selects `<input>` elements with a "readonly" attribute specified |
    | :read\-write | input:read\-write | Selects `<input>` elements with no "readonly" attribute |
    | :required | input:required | Selects `<input>` elements with a "required" attribute specified |
    | :root | root | Selects the document's root element |
    | :target | \#news:target | Selects the current active \#news element \(clicked on a URL containing that anchor name\) |
    | :valid | input:valid | Selects all `<input>` elements with a valid value |
    | :visited | a:visited | Selects all visited links |

-   **All CSS Pseudo Elements**

    -   We add an element that looks like the original element but then we can put behind original element to add more styling

    | Selector        | Example          | Example description                                          |
    | --------------- | ---------------- | ------------------------------------------------------------ |
    | ::after         | p::after         | Insert content after every `<p>` element                     |
    | ::before        | p::before        | Insert content before every `<p>` element                    |
    | ::first\-letter | p::first\-letter | Selects the first letter of every `<p>` element              |
    | ::first\-line   | p::first\-line   | Selects the first line of every `<p>` element                |
    | ::selection     | p::selection     | Selects the portion of an element that is selected by a user |

    ```SCSS
      &__btn {
          text-transform: uppercase;
          text-decoration: none;
          display: inline-block;
          border-radius: 100px;
          //_ EASIEST - TRANSFORM
          transition: all 0.2s;
          position: relative;
          //- Type of animation, duration, mode, delay
          animation: moveInBottom 0.5s ease-out 0.75s;
          //- The animation-fill-mode applies the animation styles before the animation starts
          animation-fill-mode: backwards;

          &--white {
              @extend .header__text-box__btn;
              background-color: white;
              color: #777;
              padding: 15px 40px;
              &::after {
                  background-color: white;
              }
          }
          &:hover {
              transform: translateY(-3px);
              box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
              &::after {
                  transform: scaleX(1.4) scaleY(1.6);
                  opacity: 0;
              }
          }
          &:active {
              transform: translateY(-1px);
              box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
          }
          &::after {
              content: '';
              display: inline-block;
              height: 100%;
              width: 100%;
              border-radius: 100px;
              position: absolute;
              top: 0;
              left: 0;
              z-index: -1;
              transition: all 0.4s;
          }
      }
    ```

-   to user `::after` pseudo element, we always have to define the `content`, we can define like empty strings (but we have to define in order to display it) and also the `display` property in this case we are using `inline-block` because the original button uses `inline-block`
-   We want to look the same as the original element, that's why we defined:

    ```SCSS
      height: 100%;           //<- To use the same dimensions of the btn
      width: 100%;            //<- To use the same dimensions of the btn
      border-radius: 100px;   //<- Same border-radius of the btn
    ```

-   In order `::after` to work we need to put this new element behind the original element

    ```SCSS
      position: absolute;
      top: 0;
      left: 0;
      z-index: -1;
      transition: all 0.4s;
    ```

    ```SCSS
      &__btn {
          text-transform: uppercase;
          text-decoration: none;
          display: inline-block;
          border-radius: 100px;
          transition: all 0.2s;
          position: relative;
          animation: moveInBottom 0.5s ease-out 0.75s;
          animation-fill-mode: backwards;

          &--white {
              @extend .header__text-box__btn;
              background-color: white;
              color: #777;
              padding: 15px 40px;
              &::after {
                  background-color: blue;
              }
          }
          &::after {
              content: '';
              display: inline-block;
              height: 100%;
              width: 100%;
              border-radius: 100px;
              position: absolute;
              top: 0;
              left: 0;
              z-index: -1;
              transition: all 0.4s;
          }
      }
    ```

<h1 id='bem'>BEM (Block Element Modifier) Methodology</h1>

[Go Back to Summary](#summary)

-   Converting our existing project into BEM Methodology
-   in `index.html`:

    ```HTML
      <!DOCTYPE html>
      <html lang="en">

      <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">

          <link href="https://fonts.googleapis.com/css?family=Lato:100,300,400,700,900" rel="stylesheet">

          <link rel="stylesheet" href="css/icon-font.css">
          <link rel="stylesheet" href="css/style.css">
          <link rel="shortcut icon" type="image/png" href="img/favicon.png">

          <title>Natours | Exciting tours for adventurous people</title>
      </head>

      <body>
          <header class="header">
              <div class="header__logo-box">
                  <img class="header__logo" src="./img/logo-white.png" alt="logo">
              </div>
              <div class="header__text-box">
                  <h1 class="heading-primary">
                      <span class="heading-primary__main">Outdoors</span>
                      <span class="heading-primary__sub">is where life happens</span>
                  </h1>
                  <a href="#" class="btn btn--white btn--animated">Discover our tours</a>
              </div>
          </header>
      </body>

      </html>
    ```

-   in `style.scss`:

    ```SCSS
      *,
      *::before,
      *::after {
          margin: 0;
          padding: 0;
          box-sizing: inherit;
      }

      html {
          font-size: 62.5%;
      }

      body {
          font-family: 'Lato', sans-serif;
          font-weight: 400;
          font-size: 0.16rem;
          line-height: 1.7;
          color: #777;
          padding: 3rem;
          box-sizing: border-box;
      }

      .header {
          height: 95vh;
          background-image: linear-gradient(
                  to right bottom,
                  rgba(126, 213, 111, 0.8),
                  rgba(40, 180, 131, 0.8)
              ),
              url('../img/hero.jpg');
          background-size: cover;
          background-position: top;
          clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
          position: relative;
          &__logo-box {
              position: absolute;
              top: 4rem;
              left: 4rem;
          }
          &__logo {
              height: 3.5rem;
          }
          &__text-box {
              position: absolute;
              top: 40%;
              left: 50%;
              transform: translate(-50%, -50%);
              text-align: center;
          }
      }

      .heading-primary {
          color: white;
          text-transform: uppercase;
          margin-bottom: 6rem;
          backface-visibility: hidden;
          &__main {
              display: block;
              font-size: 6rem;
              font-weight: 400;
              letter-spacing: 3.5rem;
              animation-name: moveInLeft;
              animation-duration: 1s;
              animation-timing-function: ease-in-out;
          }
          &__sub {
              display: block;
              font-size: 2rem;
              font-weight: 700;
              letter-spacing: 1.75rem;
              animation: moveInRight 1s ease-in-out;
          }
      }

      .btn {
          text-transform: uppercase;
          text-decoration: none;
          display: inline-block;
          border-radius: 10rem;
          font-size: 1.6rem;
          transition: all 0.2s;
          position: relative;
          &--white {
              background-color: white;
              color: #777;
              padding: 1.5rem 4rem;
              &::after {
                  background-color: white;
              }
          }
          &--animated {
              animation: moveInBottom 0.5s ease-out 0.75s;
              animation-fill-mode: backwards;
          }
          &:hover {
              transform: translateY(-0.3rem);
              box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.2);
              &::after {
                  transform: scaleX(1.4) scaleY(1.6);
                  opacity: 0;
              }
          }
          &:active {
              transform: translateY(-0.1rem);
              box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.2);
          }
          &::after {
              content: '';
              display: inline-block;
              height: 100%;
              width: 100%;
              border-radius: 10rem;
              position: absolute;
              top: 0;
              left: 0;
              z-index: -1;
              transition: all 0.4s;
          }
      }

      @keyframes moveInLeft {
          0% {
              opacity: 0;
              transform: translateX(-10rem);
          }
          80% {
              transform: translateX(1rem);
          }
          100% {
              opacity: 1;
              transform: translate(0);
          }
      }

      @keyframes moveInRight {
          0% {
              opacity: 0;
              transform: translateX(10rem);
          }
          80% {
              transform: translateX(-1rem);
          }
          100% {
              opacity: 1;
              transform: translate(0);
          }
      }

      @keyframes moveInBottom {
          0% {
              opacity: 0;
              transform: translateY(10rem);
          }
          100% {
              opacity: 1;
              transform: translate(0);
          }
      }
    ```

<h1 id='sass'>Sass</h1>

[Go Back to Summary](#summary)

-   With **Sass** we have:
    -   **Variables**: for reusable values such as colors, font-sizes, spacing, etc.
    -   **Nesting**: to nest selectors inside one of another, allowing us to write less code;
    -   **Operators**: for mathematical operations right inside of CSS
    -   **Partials and Imports**: to write CSS in different files and importing them all into one single file
    -   **Mixins**: to write reusable pieces of CSS code
    -   **Functions**: similar to mixins, with the difference that they produce a value that can be used
    -   **Extends**: to make different selectors inherit declarations that are common to all of them
    -   **Control Directives**: for writing complex code using conditionals and loops

<h2 id='sassvariables'>Sass Variables and Nesting</h2>

[Go Back to Summary](#summary)

-   [Final Page Link](https://codepen.io/roger-takeshita/pen/zYqvRXw?editors=1100)
-   Creating variables

    ```SCSS
      $color-primary: #f9ed69;
      $color-secondary: #f08a5d;
      $color-teritiary: #b83b5e;
      $color-text-dark: #333;
      $color-text-light: #eee;
      $width-button: 150px;
    ```

-   Built-in functions

    -   `darken($color-secondary, 15%)`
    -   `lighten($color-tertiary, 10%)`

        ```HTML
          <nav>
              <ul class="navigation">
                  <li><a href="#">About Us</a></li>
                  <li><a href="#">Pricing</a></li>
                  <li><a href="#">Contact</a></li>
              </ul>
              <div class="btn">
                  <a href="#" class="btn__main">Sign Up</a>
                  <a href="#" class="btn__hot">Get a Quote</a>
              </div>
          </nav>
        ```

        ```SCSS
          $color-primary: #f9ed69;
          $color-secondary: #f08a5d;
          $color-tertiary: #b83b5e;
          $color-text-dark: #333;
          $color-text-light: #eee;
          $width-button: 150px;

          *,
          *::before,
          *::after {
              margin: 0;
              padding: 0;
              box-sizing: inherit;
          }

          html {
              font-size: 62,5%;
          }

          body {
              box-sizing: border-box;
          }

          nav {
              margin: 3rem;
              background-color: $color-primary;

              &::after {
                  content: '';
                  clear: both;
                  display: table;
              }
          }

          .navigation {
              list-style: none;
              float: left;

              li {
                  display: inline-block;
                  margin-left: 3rem;

                  &:first-child {
                      margin: 0;
                  }

                  a {
                      text-decoration: none;
                      text-transform: uppercase;
                      color: $color-text-dark;
                  }
              }
          }

          .btn {
              float: right;

              &__main, &__hot {
                  padding: 1rem;
                  display: inline-block;
                  text-align: center;
                  border-radius: 10rem;
                  text-decoration: none;
                  text-transform: uppercase;
                  width: $width-button;
                  background-color: $color-secondary;
                  color: $color-text-light;

                  &:hover {
                      background-color: darken($color-secondary, 15%);
                  }
              }
          }
        ```

<h2 id='sassmixin'>Sass Mixin</h2>

[Go Back to Summary](#summary)

```SCSS
  $color-primary: #f9ed69;
  $color-secondary: #f08a5d;
  $color-tertiary: #b83b5e;
  $color-text-dark: #333;
  $color-text-light: #eee;
  $width-button: 150px;

  @mixin clearfix {
      &::after {
          content: '';
          clear: both;
          display: table;
      }
  }

  @mixin style-text-light ($color) {
      text-decoration: none;
      text-transform: uppercase;
      color: $color;
  }

  ...

  nav {
      margin: 3rem;
      background-color: $color-primary;
      @include clearfix;
  }

  .navigation {
      list-style: none;
      float: left;

      li {
          display: inline-block;
          margin-left: 3rem;

          &:first-child {
              margin: 0;
          }

          a {
              @include style-text-light ($color-text-dark);
          }
      }
  }

  .btn {
      float: right;

      &__main, &__hot {
          padding: 1rem;
          display: inline-block;
          text-align: center;
          border-radius: 10rem;
          width: $width-button;
          background-color: $color-secondary;
          @include style-text-light ($color-text-light);

          &:hover {
              background-color: darken($color-secondary, 15%);
          }
      }
  }
```

<h2 id='sassfunctions'>Sass Functions</h2>

[Go Back to Summary](#summary)

-   Functions are like `mixin`, the only difference is that **functions return something**

    ```SCSS
      @function divide ($arg1, $arg2) {
          @return $arg1/$arg2;
      }
    ```

-   And to use it, we just have to call it, the operation in this case returns a number, then we have to multiply by the unit in `rem/px`

    ```SCSS
      nav {
          margin: divide(60, 20) * 1rem;
          background-color: $color-primary;
          @include clearfix;
      }
    ```

<h2 id='sassextend'>Sass Extend</h2>

[Go Back to Summary](#summary)

-   `@extend` basically we can extend/inherit any style from any element
-   We can create a **placeholder** to hold certain styles

    ```SCSS
      %btn-palcehodler {
          padding: 1rem;
          display: inline-block;
          text-align: center;
          border-radius: 10rem;
          width: $width-button;
          background-color: $color-secondary;
          @include style-text-light ($color-text-light);
      }
    ```

-   And the just `@extend` to the element

    ```SCSS
      .btn {
          float: right;

          &__main, &__hot {
              @extend %btn-palcehodler;

              &:hover {
                  background-color: darken($color-secondary, 15%);
              }
          }
      }
    ```

-   The difference between creating a **placeholder** and **mixin**
    -   We only use **placeholder** if the elements are the same

<h2 id='sasspartials'>Sass Partials</h2>

[Go Back to Summary](#summary)

-   **Partials** are SCSS files that we split across our project
-   We declare as `_name.scss`

<h3 id='sassimportpartial'>Import Partials</h3>

[Go Back to Summary](#summary)

-   To import a partial we just need to use the `@import` and then specify the path to the file `@import 'base/base';`
-   Notice that we didn't need to add `_` before base and the extension. Sass compiler understands that we want to import the `_base.scss`
