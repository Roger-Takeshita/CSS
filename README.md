<h1 id='summary'>Summary</h1>

-   [CSS](#css)
    -   [Basics](#cssbasics)
        -   [Reset Project](#resetproject)
        -   [Body Element](#body)
        -   [Adding Background Image](#addingbgimage)
        -   [Positioning](#positioning)
            -   [Centering Element](#centeringelement)
        -   [Span Element](#spanelement)
    -   [Animation](#animation)
        -   [@keyframes](#keyframes)
        -   [Transition](#transition)

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
