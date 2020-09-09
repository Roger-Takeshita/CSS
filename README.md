<!-- // ~> SUMMARY -->
<h1 id='summary'>Summary</h1>

-   [Links](#links)
-   [CSS](#css)
    -   [Basics](#cssbasics)
        -   [Box-Sizing - Reset Project](#resetproject)
            -   [Body Element](#bodyelement)
            -   [HTML Element](#htmlelement)
        -   [@supports](#supports)
        -   [Converting Pixel to REM](#convertingpxtorem)
    -   [Styling](#styling)
        -   [Background Image](#addingbgimage)
            -   [clip-path: polygon()](#clipathpolygon)
            -   [Alternative to clip-path](#alternativetoclippath)
        -   [Background Video](#backgroundvideo)
        -   [Advanced linear-gradient()](advancedgradient)
        -   [Positioning](#positioning)
            -   [Centering Element - Absolute Position](#centeringelement)
        -   [Span Element](#spanelement)
        -   [Column Property](#columnproperty)
            -   [Hyphens](#hyphens)
        -   [-webkit-background-clip - Background Text Styling](#webkitbackgroundclip)
        -   [Outline vs Border](#outlinevsborder)
        -   [Figure Element](#figureelement)
            -   [Float](#float)
        -   [Filters](#filter)
        -   [Selector/Combinator](#csscombinator)
            -   [Descendent Selector](#descendantselector)
            -   [> Direct Child Selector](#childselector)
            -   [+ Adjacent Sibling Selector](#adjacentsiblingselector)
            -   [~ General Sibling Selector](#generalsibligselector)
            -   [[] Attribute Selector](#attributeselector)
        -   [Responsive Images](#responsiveimages)
            -   [Density Switching](#densityswitching)
            -   [Art Direction](#artdirection)
        -   [Flexbox](#flexbox)
        -   [Grid](#grid)
            -   [Basics Grid](#basicsgrid)
            -   [Grid Start / End](#gridstartend)
            -   [Naming Grid](#naminggrid)
            -   [Naming Grid Area](#naminggridarea)
            -   [Implicit vs Explicit](#implicitvsexplicit)
            -   [Align Grid Items](#aligngriditems)
            -   [Fixing Grid Holes](#fixinggridholes)
            -   [max-content](#maxcontent)
            -   [min-content](#mincontent)
            -   [minmax()](#minmaxgrid)
            -   [Auto-Fit and Auto-Fill](#autofitautofill)
    -   [Animation](#animation)
        -   [@keyframes](#keyframes)
        -   [Transition](#transition)
            -   [Multiple Transitions](#multipletransitions)
            -   [Pseudo Classes](#pseudoclasses)
            -   [Pseudo Elements](#pseudoelements)
            -   [Chaining Pseudo Classes - Validation](#chainingpsudeoclasses)
            -   [Cubic-Bezier](#cubicbezier)
        -   [Advanced Hover](#advancedhover)
            -   [Hover Selecting Modifiers](#hoverselectingmodifier)
        -   [Rotating](#rotating)
            -   [Perspective](#perspective)
            -   [Backface-visibility](#backfacevisibility)
    -   [Popup](#popup)
        -   [Target](#target)
-   [BEM (Block Element Modifier) Methodology](#bem)
-   [Sass](#sass)
    -   [Sass Variables and Nesting](#sassvariables)
    -   [Sass Mixin](#sassmixin)
    -   [Sass Functions](#sassfunctions)
    -   [Sass Extend](#sassextend)
    -   [Sass Partials](#sasspartials)
        -   [Import Partials](#sassimportpartial)
-   [Responsive Web Design](#responsivedesign)
    -   [Mobile First](#mobilefirst)
    -   [Media Queries Sizes](#mediaqueriessizes)
    -   [Media Query With SASS](#mediaquerysass)

<!-- // ~> LINKS -->
<h1 id='links'>Links</h1>

[Go Back to Summary](#summary)

-   [Can I Use?](https://caniuse.com/)
-   [Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
-   [Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
-   [Cursor](https://www.w3schools.com/cssref/playit.asp?filename=playcss_cursor&preval=cell)
-   [cubic-bezier](https://cubic-bezier.com/#.17,.67,.83,.67)
-   [Easing Functions](https://easings.net/)

<!-- // ~> CSS -->
<h1 id='css'>CSS</h1>

<!-- // ~~> BASICS -->
<h2 id='cssbasics'>Basics</h2>

<!-- // ~~~> Box-Sizing -->
<h3 id='resetproject'>Box-Sizing - Reset Project</h3>

[Go Back to Summary](#summary)

-   [box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)
-   [box-sizing: border-box explained](https://www.youtube.com/watch?v=WlGQdgy-M6w)
-   Before start styling our website, a good practice is to reset all the browser parameters. Each browser has different parameters and we want to display our website the same way in all browsers.

    -   By default in the `CSS box model`, the `width` and `height` you assign to an element is applied only to the element's content box. If the element has any border or padding, this is then added to the `width` and `height` to arrive at the size of the box that's rendered on the screen. This means that when you set `width` and `height`, you have to adjust the value you give to allow for any border or padding that may be added.
        -   **content-box** gives you the default CSS box-sizing behavior. If you set an element's width to 100 pixels, then the element's content box will be 100 pixels wide, and the width of any border or padding will be added to the final rendered width, making the element wider than 100px.
        -   **border-box** tells the browser to account for any border and padding in the values you specify for an element's width and height. If you set an element's width to 100 pixels, that 100 pixels will include any border or padding you added, and the content box will shrink to absorb that extra width. This typically makes it much easier to size elements.
    -   the `box-sizing: border-box;` removes the box margin and padding to not be considered in the total `width` or total `height` of the element
    -   a good practice instead of just selecting the all elements (`*`), we can select the `::before` and `::after` pseudo elements, and define the reset parameters

    ```SCSS
      *,
      *::before,
      *::after {
          margin: 0;
          padding: 0;
          box-sizing: inherit;
      }

      html {
          box-sizing: border-box;
      }
    ```

<h4 id='bodyelement'>Body Element</h4>

-   in the `body` we can define the `font-family`, instead of the generic `*`

    ```SCSS
      body {
          font-family: 'Lato', sans-serif;
          font-weight: 400;
          font-size: 0.16rem;
          line-height: 1.7;
          color: #777;
          padding: 3rem;
      }
    ```

<h4 id='htmlelement'>HTML Element</h4>

-   another good practice is to define the default `font-size` of the project

        -   To do so, we define in the `html` tag, and we set to `10px` so we can easily convert into REM

        ```SCSS
          html {
              box-sizing: border-box;
              font-size: 10px;
          }
        ```

        -   We could also use in **%**, we just have to convert the `10px`.
        -   By default the `font-size` is `16px`, so we just need to divide `10px/16px = 0.625` or `62.5%`

        ```SCSS
          html {
              box-sizing: border-box;
              font-size: 62.5%;
          }
        ```

<!-- // ~~~> @supports -->
<h3 id='supports'>@supports - Media Query</h3>

[Go Back to Summary](#summary)

-   [Can I Use?](https://caniuse.com/)
-   The `@supports` checks if the browser supports certain feature, this might be handy if certain feature is not supported by a certain browser
-   For example the `backdrop-filter` is not supported by Internet Explorer and Firefox (needs to be enabled by the user in the Firefox config - not enabled by default)

    -   [backdrop-filer compatibility](https://developer.mozilla.org/en-US/docs/Web/CSS/backdrop-filter)

    ```SCSS
      @supports ((-webkit-backdrop-filter: blur(10px)) or(backdrop-filter: blur(10px);
      )) {
          // -webkit-backdrop-filter: blur(10px); // Add support for Safari
          backdrop-filter: blur(10px); // Other browser Chrome, Edge
          background-color: rgba($color-black, 0.3);
      }
    ```

-   Adding a SVG using css, instead of using the html

    -   With **supports** we always have to specify a value, could be nothing like `url()`

    ```SCSS
      &__item {
          flex: 0 0 50%;
          margin-bottom: 0.7rem;

          &::before {
              content: '';
              display: inline-block;
              height: 1rem;
              width: 1rem;
              margin-right: 0.7rem;

              //! Older browsers
              background-image: url(../img/chevron-thin-right.svg);
              background-size: cover;

              //! Newer Browsers - masks
              @supports (-webkit-mask-image: url()) or (mask-image: url()) {
                  background-color: var(--color-primary);
                  -webkit-mask-image: url(../img/chevron-thin-right.svg);
                  -webkit-mask-size: cover;
                  mask-image: url(../img/chevron-thin-right.svg);
                  mask-size: cover;
                  background-image: none;
              }
          }
      }
    ```

<!-- // ~~~> Converting Pixel to REM -->
<h3 id='convertingpxtorem'>Converting Pixel to REM</h3>

[Go Back to Summary](#summary)

-   If we have set our `html` to `font-size: 16px` this means that `1rem` is equal to `16px`
-   So we can convert `rem` using the **rule of three**

|  px  |    rem     |
| :--: | :--------: |
| 15px | 0.9375 rem |
| 16px |   1 rem    |
| 17px | 1.0625 rem |

<!-- // ~~> STYLING -->
<h2 id='styling'>Styling</h2>

<!-- // ~~~> Background Image -->
<h3 id='addingbgimage'>Background Image</h3>

[Go Back to Summary](#summary)

-   To an image as a background we simply call `background-image: url(<relative_path/image>)`

-   With `background-image` we also can specify the gradient property
-   Before the `url()` we can specify `linear-gradient(direction, from-color, to-color)`
    -   Ideally we specify the color as `rgba` so we we can set the **opacity**
    -   We can specify more than one direction, such as `to right bottom`
-   `background-size: cover;` tries to fit the image inside the box to use the whole available width. If we change the **viewport** the image will be resized until the height hits e available height of the element
-   `background-position: top;` ensures that the top of the image is always visible, and the bottom is cropped if bigger the than the available space

    ```SCSS
      .header {
          height: 95vh;
          background-image: linear-gradient(
                  to right bottom,
                  rgba($color-primary-light, 0.8),
                  rgba($color-primary-dark, 0.8)
              ),
              url('../img/hero.jpg');
          background-size: cover;
          background-position: top;
      }
    ```

<h4 id='clipathpolygon'>clip-path: polygon()</h4>

-   `clip-path: polygon(x y, x y, x y, x y)` displays only the defined area of the image

-   [clip-path maker - Website](https://bennettfeely.com/clippy/)

    ```SCSS
      .header {
          -webkit-clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
          clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
      }
    ```

-   `-webkit-clip-path` to support different browsers

<h4 id='alternativetoclippath'>Alternative to clip-path</h4>

-   An alternative to clip path, if we want to just **skew** the image by **-7 degrees**
-   `transform: skewY(-7deg);`
-   The only problem is all the nested elements will be skewed by **-7 degrees**
-   One easy and better way to fix this, is to **select all direct child of an element** and skew back **7 degrees**

    ```SCSS
      & > * {
          transform: skewY(7deg);
      }
    ```

<!-- // ~~~> Background Video -->
<h3 id='backgroundvideo'>Background Video</h3>

[Go Back to Summary](#summary)

-   The `<video>` tag is used to embed video content in a document, such as a movie clip or other video streams.
-   The `<video>` tag contains one or more `<source>` tags with different video sources. The browser will choose the first source it supports.
-   The text between the `<video>` and `</video>` tags will only be displayed in browsers that do not support the `<video>` element.
-   There are three supported video formats in HTML: **MP4**, **WebM**, and **OGG**.
-   List of supported browser

| Browser   | MP4 | WebM | Ogg |
| --------- | --- | ---- | --- |
| Edge / IE | YES | NO   | NO  |
| Chrome    | YES | YES  | YES |
| Firefox   | YES | YES  | YES |
| Safari    | YES | NO   | NO  |
| Opera     | YES | YES  | YES |

-   how to use `<video>` tag:

-   First create the a `<section>`/`<div>` tag to display the video as a background
-   Then create a container for the video

    -   Inside this container, we crate our `<video>` tag, **without the src** property
        -   Here we can define other properties like `autoplay`, `mute`, `loop`...
    -   Inside the `<video>` tag, we can define `<source>`
        -   In our case we are defining 2 types of video (just in case the browser doesn't support the video format)
        -   If the browser doesn't support any of the available formats, then it will display the msg `Your browser is not supported!`

    ```HTML
      <section class="section-stories">
          <div class="bg-video">
              <video class="bg-video__content" autoplay muted loop>
                  <source src="img/video.mp4" type="video/mp4">
                  <source src="img/video.webm" type="video/webm">
                  Your browser is not supported!
              </video>
          </div>
      </section>
    ```

    ```SCSS
      .section-stories {
          padding: 15rem 0;
          position: relative;
      }
      .bg-video {
          position: absolute;
          top: 0;
          left: 0;
          height: 100%;
          width: 100%;
          z-index: -1;
          opacity: 0.15;
          overflow: hidden;

          &__content {
              height: 100%;
              width: 100%;
              object-fit: cover;
          }
      }
    ```

-   in this case `.bg-video` we give `position: absolute;` in relation to the parent element `.section-stories` (`position: relative`), then we assign the `top` and `left`
    -   then we define to use the max available space (width and height)
    -   `z-index: -1;` just in case we are using displaying another element in front of the video
    -   `opacity: 0.15;` to fade the video
    -   `overflow: hidden;` to hide the overflowing video, just in case we have some
-   Then for the actual video
    -   we give 100% of the available space (width and height)
    -   `object-fit: cover;` to use all the available space without losing the aspect ratio

<!-- // ~~~> Advanced linear-gradient() -->
<h3 id='advancedgradient'>Advanced linear-gradient()</h3>

[Go Back to Summary](#summary)

-   An alternative to `clip-path` is the `linear-gradient()`, where we can define:

-   The angle of the gradient
-   then we define the initial color (0%)
-   the middle color at 50%
-   the end color will be applied the last color until the end (100%)

    -   So if we define 2 colors at the same point, we don't give space enough to create the gradient

    ```SCSS
      .book {
          background-image: linear-gradient(
                  105deg,
                  rgba($color-white, 0.85) 0%,
                  rgba($color-white, 0.85) 50%,
                  transparent 50%
              ),
              url('../img/nat-10.jpg');
          background-size: cover;
          border-radius: 0.3rem;
          box-shadow: 0 1.5rem 4rem rgba($color-black, 0.2);
          height: 50rem;
      }
    ```

<!-- // ~~~> Positioning -->
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
          position: relative;

          &__logo-box {
              position: absolute;
              top: 4rem;
              left: 4rem;
          }
          &__text-box {
              position: absolute;
              top: 40%;
              left: 50%;
              transform: translate(-50%, -50%);
              text-align: center;
          }
      }
    ```

<h4 id='centeringelement'>Centering Element - Absolute Position</h4>

-   To center an element in the middle of the screen, one option is to use the **absolute** position

    ```SCSS
      .header {
          height: 95vh;
          position: relative;

          &__text-box {
              position: absolute;
              top: 40%;
              left: 50%;
              transform: translate(-50%, -50%);
              text-align: center;
          }
      }
    ```

<!-- // ~~~> Span Element -->
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

<!-- // ~~~> Column Property -->
<h3 id='columnproperty'>Column Property</h3>

[Go Back to Summary](#summary)

-   the `column-count` property specifies the number of the columns that an element can have. Instead of creating another `div` to divide a paragraph into 2 columns

-   `column-gap` property specifies the gab between the columns, if we defined a specific `font-size` to the element, this will be the `rem` value to be considered.
-   `column-rule` property creates a line between the columns

```SCSS
  -moz-column-count: 2;
  -moz-column-gap: 4rem;
  -moz-column-rule: 1px solid $color-grey-light-2;
  column-count: 2;
  column-gap: 4rem;
  column-rule: 1px solid $color-grey-light-2;

  -moz-hyphens: auto;
  -ms-hyphens: auto;
  -webkit-hyphens: auto;
```

<h4 id='hyphens'>Hyphens</h4>

[Go Back to Summary](#summary)

-   `hyphens` property adds **hyphens**(`-`) between long words
-   `hyphens: none;`
-   `hyphens: manual;`
-   `hyphens: auto;`
-   To `hyphens` make it work, we need to define the language of the page, inside of the `html` tag
    -   `<html lang="en">`

<!-- // ~~~> -webkit-background-clip -->
<h3 id='webkitbackgroundclip'>-webkit-background-clip - Background Text Styling</h3>

[Go Back to Summary](#summary)

-   The `background-clip` CSS property sets whether an element's background extends underneath its border box, padding box, or content box.
-   When we set `background-clip: text;` the background is clipped exactly where is the text, so we can set the text to `transparent` just to show the background.

-   Why would we do something like that? Well we can define the background to `background-image: linear-gradient();` then our text would be with gradient colors

    ```SCSS
      .heading-secondary {
          font-size: 3.5rem;
          text-transform: uppercase;
          font-weight: 700;
          display: inline-block;
          background-image: linear-gradient(
              $color-primary-light,
              $color-primary-dark
          );
          -webkit-background-clip: text;
          color: transparent;
      }
    ```

<!-- // ~~~> Outline vs Border -->
<h3 id='outlinevsborder'>Outline vs Border</h3>

[Go Back to Summary](#summary)

-   `outline` is similar to `border`, we can active the same result with

    ```SCSS
      div {
        outline: 1.5rem solid red;
      }
    ```

    ```SCSS
      div {
        border: 1.5rem solid red;
      }
    ```

-   The difference really shines when we need to add an offset for the border

    ```SCSS
      &__photo {
          width: 55%;
          box-shadow: 0 1.5rem 4rem rgba($color-black, 0.4);
          border-radius: 0.2rem;
          position: absolute;
          z-index: 10;
          outline-offset: 2rem;
          transition: all 0.2s;

          &:hover {
              transform: scale(1.05) translateY(-0.5rem);
              box-shadow: 0 2rem 4rem rgba($color-black, 0.5);
              z-index: 20;
              outline: 1.5rem solid $color-primary;
          }
      }
    ```

<!-- // ~~~> Figure Element -->
<h3 id='figureelement'>Figure Element</h3>

[Go Back to Summary](#summary)

-   The HTML `<figure>` **(Figure With Optional Caption) element** represents self-contained content, potentially with an optional caption, which is specified using the (`<figcaption>`) element. The figure, its caption, and its contents are referenced as a single unit.

    ```HTML
      <figure>
          <img src="/media/examples/elephant-660-480.jpg"
              alt="Elephant at sunset">
          <figcaption>An elephant at sunset</figcaption>
      </figure>
    ```

-   To work with `<figure>` we have to follow the define the following boilerplate

-   `width` and `height`
-   `float` position, and float only works with defined width and height
-   `shape-outside`, could be a **polygon**, **circle**...

    -   **internet explorer doesn't support this property**
    -   the `shape-outside` only defines the shape around the element
    -   if we want to look like a circle we need to user the `clip-path` property

    ```HTML
      <div class="story">
          <figure class="story__shape">

          </figure>
          <div class="story__text">
              <h3 class="heading-tertiary u-margin-bottom-small">
                  I had the best weekend with my family
              </h3>
              <p>
                  Lorem ipsum dolor sit amet consectetur adipisicing elit. Beatae nulla eos corrupti
                  exercitationem quos! Non corrupti, culpa deleniti quisquam commodi quam minima fugit nihil
                  velit ab doloremque recusandae natus magni! Lorem ipsum dolor sit, amet consectetur
                  adipisicing elit. Expedita quo dolor et molestias, qui illo temporibus perferendis iure
                  eveniet aperiam similique nobis fugiat corrupti ab deleniti, laborum reiciendis blanditiis
                  at.
              </p>
          </div>
      </div>
    ```

    ```SCSS
      .story {
          width: 75%;
          margin: 0 auto;
          box-shadow: 0 3rem 6rem rgba($color-black, 0.1);
          background-color: $color-white;
          border-radius: 0.3rem;
          padding: 6rem;
          padding-left: 9rem;
          font-size: $default-font-size;

          &__shape {
              width: 15rem;
              height: 15rem;
              float: left;
              background-color: red;
              -webkit-shape-outside: circle(50% at 50% 50%);
              shape-outside: circle(50% at 50% 50%);
              -webkit-clip-path: circle(50% at 50% 50%);
              clip-path: circle(50% at 50% 50%);
          }
      }
    ```

<h4 id='float'>Float</h4>

-   When we are working with `float` property, the best way to center the object is using `transform`
-   if we try to user `margin` or `padding` this could mess up with our styling

<!-- // ~~~> Filters -->
<h3 id='filter'>Filters</h3>

[Go Back to Summary](#summary)

-   The **filter** CSS property applies graphical effects like blur or color shift to an element. Filters are commonly used to adjust the rendering of images, backgrounds, and borders.
-   Included in the CSS standard are several functions that achieve predefined effects. You can also reference an SVG filter with a URL to an SVG filter element.

    ```SCSS
      /* <filter-function> values */
      filter: blur(5px);
      filter: brightness(0.4);
      filter: contrast(200%);
      filter: drop-shadow(16px 16px 20px blue);
      filter: grayscale(50%);
      filter: hue-rotate(90deg);
      filter: invert(75%);
      filter: opacity(25%);
      filter: saturate(30%);
      filter: sepia(60%);

      /* Multiple filters */
      filter: contrast(175%) brightness(3%);
    ```

<!-- // ~~~> Selector/Combinator -->
<h3 id='csscombinator'>Selector/Combinator</h3>

[Go Back to Summary](#summary)

-   A CSS selector can contain more than one simple selector. Between the simple selectors, we can include a combinator.
-   There are four different combinators in CSS:

-   descendant selector (`space`)
-   child selector (`>`)
-   adjacent sibling selector (`+`)
-   general sibling selector (`~`)

-   We can use theses combinations to style the adjacent element

    ```SCSS
      &__label {
          font-size: 1.2rem;
          font-weight: 700;
          margin-left: 2rem;
          margin-top: 0.7rem;
          display: block;
          transition: all 0.3s;
      }
      &__input:placeholder-shown + &__label {
          opacity: 0;
          visibility: hidden;
          transform: translateY(-4rem);
      }
    ```

    ```HTML
      <form action="#" class="form">
          <div class="u-margin-bottom-medium">
              <h2 class="heading-secondary">
                  Start booking now
              </h2>
          </div>
          <div class="form__group">
              <input type="text" class="form__input" placeholder="Full name" required
                  autocomplete="off" id="name">
              <label for="name" class="form__label">Full name</label>
          </div>
          <div class="form__group">
              <input type="email" class="form__input" placeholder="Email address" required
                  autocomplete="off" id="email">
              <label for="email" class="form__label">Email address</label>
          </div>
      </form>
    ```

    ```SCSS
      .form {
          &__group:not(:last-child) {
              margin-bottom: 2rem;
          }
          &__input {
              font-size: 1.5rem;
              font-family: inherit;
              color: inherit;
              padding: 1.5rem 2rem;
              border-radius: 0.2rem;
              background-color: rgba($color-white, 0.5);
              border: none;
              border-bottom: 0.3rem solid transparent;
              width: 40%;
              display: block;
              transition: all 0.3s;

              &:focus {
                  outline: none;
                  box-shadow: 0 1rem 2rem rgba($color-black, 0.1);
                  border-bottom: 0.3rem solid $color-primary;
              }
              &:focus:invalid {
                  border-bottom: 0.3rem solid $color-secondary-dark;
              }
              &::-webkit-input-placeholder {
                  color: $color-grey-dark-2;
              }
              &:valid {
                  border-bottom: 0.3rem solid $color-primary;
              }
              &:invalid {
                  border-bottom: 0.3rem solid $color-secondary-dark;
              }
          }
          &__label {
              font-size: 1.2rem;
              font-weight: 700;
              margin-left: 2rem;
              margin-top: 0.7rem;
              display: block;
              transition: all 0.3s;
          }
          &__input:placeholder-shown + &__label {
              opacity: 0;
              visibility: hidden;
              transform: translateY(-4rem);
          }
      }
    ```

-   Creating a radio button using **span** and **input**

    ```HTML
      <div class="form__group">
          <div class="form__radio-group">
              <input type="radio" class="form__radio-input" id="small" name="size">
              <label for="small" class="form__radio-label">
                  <span class="form__radio-button"></span>
                  Small tour group
              </label>
          </div>
          <div class="form__radio-group">
              <input type="radio" class="form__radio-input" id="large" name="size">
              <label for="large" class="form__radio-label">
                  <span class="form__radio-button"></span>
                  Large tour group
              </label>
          </div>
      </div>
    ```

    ```SCSS
      .form {
          &__radio-group {
              width: 20%;
              display: inline-block;
          }
          &__radio-label {
              font-size: $default-font-size;
              cursor: pointer;
              position: relative;
              padding-left: 5rem;
          }
          &__radio-button {
              height: 3rem;
              width: 3rem;
              border: 0.5rem solid $color-primary;
              border-radius: 50%;
              display: inline-block;
              position: absolute;
              top: -0.4rem;
              left: 0;

              &::after {
                  height: 1.3rem;
                  width: 1.3rem;
                  content: '';
                  display: inline-block;
                  border-radius: 50%;
                  position: absolute;
                  top: 50%;
                  left: 50%;
                  transform: translate(-50%, -50%);
                  background-color: $color-primary;
                  opacity: 0;
                  transition: opacity 0.2s;
              }
          }
          &__radio-input {
              display: none;
          }
          &__radio-input:checked ~ &__radio-label &__radio-button::after {
              opacity: 1;
          }
      }
    ```

<h4 id='descendantselector'>Descendent Selector</h4>

-   The descendant selector matches **all elements** that are **descendants** of a specified element.

    ```SCSS
      .descendant p {
        background-color: yellow;
      }
      // Will match all <p> inside the <div>
    ```

    ```HTML
      <div class="descendant">
          <p> This text is yellow</p>
          <div class="random-class-1">
              <p> This text is yellow</p>
              <div class="random-class-2">
                  <p> This text is yellow</p>
              </div>
          </div>
      </div>
    ```

<h4 id='childselector'>> Direct Child Selector</h4>

-   The child selector selects all elements that are the **direct child** of a specified element.

    ```CSS
      .direct-child > p {
        background-color: yellow;
      }
    ```

    ```HTML
      <div class="direct-child">
          <p> This text is yellow</p>
          <div class="random-class-1">
              <p> This text is NOT yellow</p>
              <div class="random-class-2">
                  <p> This text is NOT yellow</p>
              </div>
          </div>
          <p> This text is yellow</p>
      </div>
    ```

<h4 id='adjacentsiblingselector'>+ Adjacent Sibling Selector</h4>

-   The adjacent sibling selector selects all elements that are the adjacent siblings of a specified element.
-   Sibling elements must have the same parent element, and **adjacent** means **immediately following**.

-   It looks for sibiling that comes before, that's why the first box is white, because it doesn't have a sibling before with the class `.box`

    ```CSS
      .adjacent-sibling {
          display: flex;
      }

      .box {
          height: 60px;
          width: 60px;
          margin: 10px;
          border: 2px solid black;
          display: flex;
          justify-content: center;
          align-items: center;
      }

      .adjacent-sibling .box + .box {
          background-color: yellow;
      }
    ```

    ```HTML
      <div class="adjacent-sibling">
          <div class="box">White</div>
          <div class="box">Yellow</div>
          <div class="box">Yellow</div>
          <div class="box">Yellow</div>
      </div>
    ```

    ```HTML
      <div class="adjacent-sibling">
          <div class="box">White</div>
          <div class="box">Yellow</div>
          <div class="something-else">Something else</div>
          <div class="box">white</div>
          <div class="box">Yellow</div>
      </div>
    ```

<h4 id='generalsibligselector'>~ General Sibling Selector</h4>

-   The general sibling selector selects all elements that are siblings of a specified element.
-   It works similar to **adjacent sibling**, It looks for sibiling that comes before, that's why the first box is white, because it doesn't have a sibling before with the class `.box`, but with **general sibling** anything before has to be the selector

    ```CSS
      .general-sibling {
          display: flex;
      }

      .box {
          height: 60px;
          width: 60px;
          margin: 10px;
          border: 2px solid black;
          display: flex;
          justify-content: center;
          align-items: center;
      }

      .general-sibling .box ~ .box {
          background-color: yellow;
      }
    ```

    ```HTML
      <div class="general-sibling">
          <div class="box">White</div>
          <div class="box">Yellow</div>
          <div class="something-else">Something else</div>
          <div class="box">Yellow</div>
          <div class="box">Yellow</div>
      </div>
    ```

<h4 id='attributeselector'>[] Attribute Selector</h4>

```HTML
  <div class="attributes">
    <a href="https://www.google.com" class="link-one">Google</a>
    <a href="https://www.google.ca" class="link-two">Google Canada</a>
    <a href="about.html" class="link-three">About Page</a>
    <a href="http://rogertakeshita.com" class="link-four" target="_blank">Roger</a>
    <a href="ebook.pdf" class="link-five">PDF File</a>
    <a href="#" class="another-link">Another Link</a>
  </div>
```

-   **Targeting an Attribute**

    -   in this case we are selecing anthing that has the attribute `target`

    ```SCSS
      [target] {
          color: pink;
      }
    ```

    -   now we are more specific selecting all `<a>` that have an attribute `target`

    ```SCSS
      a[target] {
          color: pink;
      }
    ```

-   **Targeting an Attribute Equal to Something =**

    -   even more specific, all `<a>` that have an attribute `target` equals to `_blank`
    -   The right part (`_blank`) has to be a **exactly match**

    ```SCSS
      a[target="_blank"] {
          color: pink;
      }

      a[href="about.html"] {
          color: red;
      }
    ```

-   **Targeting an Attribute That Has Somehing Equal To |**

    -   It will look after an attribute that starts with what we have, **separatated by -**

    ```SCSS
      a[class|='another'] {
          color: purple;
      }

      a[class|='link'] {
          color: green;
      }

      // This won't work
      a[class|='anotherLink'] {
          color: purple;
      }
    ```

-   **Targeting an Attribute Beginning With ^**

    ```SCSS
      a[href^='http'] {
          color: orange;
      }
    ```

-   **Targeting an Attribute That Has Anthhing Equals To \***

    -   It will target anthing that has `google`, it doesn't matter if it's in the beginning or in the end

    ```SCSS
      a[href*='google'] {
          color: orange;
      }
    ```

-   **Targeting an Attribute Ending With \$**

    ```SCSS
      a[href$='.ca'] {
          color: blue;
      }
    ```

    -   We could add an image `after` external links

    ```SCSS
      a[target$='_blank']::after {
          content: url('../../your_img.png');
      }
    ```

-   Instead of creating a class so select a specific element(s)
-   we can select using `[class^="col-"]`

    -   Where `class` is the they of attribute that we are targeting
    -   `^=` select classes that starts with
        -   `*=` select classes that contains anything equals
        -   `$=` select classes that ends with
    -   `"col-"` the name of the variable

-   Another cool command is the **negation** (`:not()`)

    ```SCSS
      &:not(:last-child) {
          margin-bottom: $gap-vertical;
      }
    ```

-   in `index.html`

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

          <title>Custom Grid With Floats</title>
      </head>

      <body>
          <section class="grid-test">
              <div class="grid-test__row">
                  <div class="col-1-of-2">Col 1 of 2</div>
                  <div class="col-1-of-2">Col 1 of 2</div>
              </div>
              <div class="grid-test__row">
                  <div class="col-1-of-3">Col 1 of 3</div>
                  <div class="col-1-of-3">Col 1 of 3</div>
                  <div class="col-1-of-3">Col 1 of 3</div>
              </div>
              <div class="grid-test__row">
                  <div class="col-1-of-3">Col 1 of 3</div>
                  <div class="col-2-of-3">Col 2 of 3</div>
              </div>
              <div class="grid-test__row">
                  <div class="col-1-of-4">Col 1 of 4</div>
                  <div class="col-1-of-4">Col 1 of 4</div>
                  <div class="col-1-of-4">Col 1 of 4</div>
                  <div class="col-1-of-4">Col 1 of 4</div>
              </div>
              <div class="grid-test__row">
                  <div class="col-1-of-4">Col 1 of 4</div>
                  <div class="col-1-of-4">Col 1 of 4</div>
                  <div class="col-2-of-4">Col 2 of 4</div>
              </div>
              <div class="grid-test__row">
                  <div class="col-1-of-4">Col 1 of 4</div>
                  <div class="col-3-of-4">Col 3 of 4</div>
              </div>
          </section>
      </body>

      </html>
    ```

-   in `style.scss`

    ```SCSS
      .grid-test {
          &__row {
              max-width: $grid-width;
              background-color: #eee;
              margin: 0 auto;

              &:not(:last-child) {
                  margin-bottom: $gap-vertical;
              }

              @include clearfix;

              [class^='col-'] {
                  background-color: orangered;
                  float: left;
                  text-align: center;
                  color: $color-white;
                  height: 5rem;
                  font-size: 2rem;
                  display: flex;
                  justify-content: center;
                  align-items: center;

                  &:not(:last-child) {
                      margin-right: $gap-horizontal;
                  }
              }

              .col-1-of-2 {
                  width: calc((100% - #{$gap-horizontal}) / 2);
              }

              .col-1-of-3 {
                  width: calc((100% - 2 * #{$gap-horizontal}) / 3);
              }

              .col-2-of-3 {
                  width: calc(
                      (2 * ((100% - 2 * #{$gap-horizontal})) / 3) + #{$gap-horizontal}
                  );
              }

              .col-1-of-4 {
                  width: calc((100% - 3 * #{$gap-horizontal}) / 4);
              }

              .col-2-of-4 {
                  width: calc(
                      (2 * ((100% - 3 * #{$gap-horizontal})) / 4) + #{$gap-horizontal}
                  );
              }

              .col-3-of-4 {
                  width: calc(
                      (3 * ((100% - 3 * #{$gap-horizontal})) / 4) + 2 * #{$gap-horizontal}
                  );
              }
          }
      }
    ```

<!-- // ~~~> Responsive Images -->
<h3 id='responsiveimages'>Responsive Images</h3>

[Go Back to Summary](#summary)

<h4 id='densityswitching'>Density Switching</h4>

-   On our html we can define two types of images for low density screens (`1x`) and high density screens (`2x`)
-   We can do using the `srcset` atribute

    ```HTML
      <img srcset="img/logo-green-2x.png 1x, img/logo-green-2x.png 2x" alt="Full logo" class="footer__logo">
    ```

<h4 id='artdirection'>Art Direction</h4>

-   It's to use different images depending on the size of the viewport, we can force using `<picture>` with the condition `<source>` where we can specify the media query break point.

    ```HTML
      <picture class="footer__logo">
          <source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x"
              media="(max-width: 37.5rem)">
          <img
              srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x"
              alt="Full logo"
              src="img/logo-green-2x.png"
          >
      </picture>
    ```

    -   basicallly we tell the browser to use `srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x"` if the browser is less than 37.rem (600px) `media="(max-width: 37.5rem)"`
    -   otherwise, use `<img srcset="img/logo-green-2x.png 1x, img/logo-green-2x.png 2x" alt="Full logo">`
    -   `src="img/nat-1-large.jpg"` in the end we add the source of the image, just in case the user is using an older browser and doesn't support `srcset` and `sizes` (newer attributes)

<h4 id='resolutionswitching'>Resolution Switching</h4>

-   Unlike **art direction** that **forces the browser to use a certain image according to a midia query**, the **resolution switching** uses the viewport and the pixel density to choose the best image
-   Just like the density switching we are going to use `srcset` with the help of the width descriptor (instead of the density descriptor (`1x`, `2x`))

    ```HTML
        <img srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w"
             sizes="(max-width: 56.25em) 20vw, (max-width: 37.5em) 30vw, 300px"
             alt="Photo 1"
             class="composition__photo composition__photo--p1"
             src="img/nat-1-large.jpg"
        >
    ```

    -   `900px/16px = 56.25em`
    -   `600px/16px = 37.5em`
    -   `srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w"` we define the actual image width size
    -   `sizes="(max-width: 56.25em) 20vw, (max-width: 37.5em) 30vw, 300px"` the we have to inform the browser what is the corresponding **image** size for the `viewport` at `56.25em`
        -   We basically divided the `desired final size/view port`, in other words, `171px/900px ≈ 0.2`
        -   We add as many break points that we need, and in the end we add the default size (`300px`)
    -   `src="img/nat-1-large.jpg"` in the end we add the source of the image, just in case the user is using an older browser and doesn't support `srcset` and `sizes` (newer attributes)

<h4 id='highresolutionscreen'>High Resolution Screen</h4>

-   we can target high resolution screen using `min-resolution` and set to `192dpi` (this is the standard value)
    -   Safari doesn't support `min-resolution`, we need to change it to `-webkit-min-device-pixel-ratio: 2` (the 2 is the pixel density)
-   and also we can **combine** with other attributes with **and**
-   or we can and **or** using a **comma**
-   in this case we want to user a high resolution image with a high resolution screen bigger than a phone screen

    -   `600px/16px = 37.5em`
    -   `2000px/16px = 125em`

    ```CSS
      @media (min-resolution: 192dpi) and (min-width: 37.5em),
             (-webkit-min-device-pixel-ratio: 2) and (min-width: 600px),
             (min-width: 125em) {
          background-image: linear-gradient(
                  to right bottom,
                  rgba($color-secondary-light, 0.8),
                  rgba($color-secondary-dark, 0.8)
              ),
              url('../img/hero.jpg');
      }
    ```

<!-- // ~~~> Flexbox -->
<h3 id='flexbox'>Flexbox</h3>

[Go Back to Summary](#summary)

-   **Container**

    -   `flex-direction: row` | row-reverse | column | column-reverse
    -   `flex-wrap: nowrap` | wrap | wrap-reverse
    -   `justify-content: flex-start` | flex-end | center | space-between | space-around | space-evenly
    -   `align-items: stretch` | flex-start | flex-end | center | baseline
    -   `align-content: stretch` | flex-start | flex-end | center | space-between | space-around

-   **Item**
    -   `align-self: auto` | strech | flex-start | flex-end | center | baseline
        -   Overwrites the property (`align-items`) for an individual element
    -   `order: 0` <integer>
        -   Sets the order from a **negative number** (first) to **positive number** (end)
    -   `flex-grow: 0` <integer>
        -   Sets the size of the element compared to other flex-grow, we could set one element to grow 2x the compared to the others
    -   `flex-shrink: 1` <integer>
        -   Sets to shrink the element compared to the size of its container, if we set to **0** it won't shrink
    -   `flex-basis: auto` <length>
        -   Sets the size of an element compared to the size of its container, we can use in **%** or **pixel**
    -   Shorthand for `flex-grow flex-shrink flex-basis`, we can simply use `flex: 0 1 auto`

<!-- // ~~~> Grid -->
<h3 id='cssgrid'>Grid</h3>

[Go Back to Summary](#summary)

<h4 id='basicsgrid'>Basics</h4>

```SCSS
    display: grid;
    // grid-template-rows: 150px 150px;
    // grid-template-rows: repeat(1, 150px) 150px;
    grid-template-rows: repeat(2, 150px);
    // grid-template-columns: 150px 150px 150px;
    // grid-template-columns: repeat(2, 150px) 150px;
    // grid-template-columns: 1fr 1fr 1fr;
    grid-template-columns: repeat(3, 1fr);

    // grid-row-gap: 30px;
    // grid-column-gap: 30px;
    grid-gap: 30px;
```

-   **fraction unit**

    -   `1fr` uccupies 100% of the available space
    -   we could use only using fractions to devide a div

-   **percentage**

    -   With **%**, css doesn't care about the available space, css only considers the total space. If we use:

    ```CSS
      .container {
          background: #eee;
          width: 1000px;
          margin: 38px auto;

          display: grid;
          grid-template-rows: repeat(2, 150px);
          grid-template-columns: 50% 1fr 1fr;
          grid-gap: 60px;
      }
    ```

    -   in this case the first gird cell will have `50%` of the `1000px`, so `500px` (not including the gap), and the rest will be `1fr` each + the `gap`, so if we increase the gap, the grid cell that is using `fr` will have less space and the grid cell that is using `%` will remain the same

<h4 id='gridstartend'>Grid Start / End</h4>

-   We use `grid-row-start`, `grid-row-end`, `grid-column-start` and `grid-column-end` to positioning a specific grid cell in the grid
-   So we could move the first item `1: Orange` to position 2x2 in a matrix 2x3

    ```CSS
      .item--1 {
          background-color: orangered;
          grid-row-start: 2;
          grid-row-end: 3;
          grid-column-start: 2;
          grid-column-end: 3;
      }
    ```

    -   A shorthand:

    ```CSS
      .item--1 {
          background-color: orangered;
          grid-row: 2 / 3;
          grid-column: 2 / 3;
      }
    ```

    -   We could also use another shorthand `grid-area`, but it's a little counfusing
    -   `grid-area: row-start / column-start / row-end / column-end`
    -   `grid-area: 2 / 2 / 3 / 3;`

<h4 id='gridspace'>Grid Space</h4>

-   We can have multiple grid cells on the same space.

    -   in this case one cell will be over another cell, to display it, we can use `z-index`

    ```CSS
      .item--5 {
          background-color: royalblue;
          grid-row: 1 / 3;
          grid-column: 3 / 4;
      }
    ```

-   We can also specify using `span` to grow the grid cell, instead having to define or count the **number of columns/rows that you want to expand**

    ```CSS
      .item--2 {
          background-color: yellowgreen;
          grid-column: 1 / span 3;
      }
    ```

-   If we don't know how many columns we have, but we want to **expand until the end**, we can use `-1`

    ```CSS
      .item--2 {
          background-color: yellowgreen;
          grid-column: 1 / -1;
      }
    ```

<h4 id='naminggrid'>Naming Grid</h4>

-   we can name the row/column using `[]` before the value, then we just need to pass the name to use the property.

    ```CSS
      .container {
          width: 1000px;
          margin: 30px auto;
          display: grid;
          grid-template-rows: [header-start] 100px [header-end box-start] 200px [box-end main-start] 400px [main-end footer-start] 100px [footer-end];
          grid-template-columns: repeat(3, [column-start] 1fr [column-end]) 200px [grid-end];
          grid-gap: 30px;
      }

      .header {
          /* grid-row: 1 / 2;
          grid-column: 1 / -1; */
          grid-row: header-start / header-start;
          grid-column: column-start 1 / grid-end;
      }

      .main-content {
          /* grid-row: 3 / 4;
          grid-column: 1 / -2; */
          grid-row: main-start / main-end;
          grid-column: column-start 1 / column-end 3;
      }

      .sidebar {
          /* grid-row: 2 / 4;
          grid-column: 4 / 5; */
          grid-row: box-start / main-end;
          grid-column: column-end 3 / grid-end;
      }

      .footer {
          /* grid-row: 4 / 5;
          grid-column: 1 / -1; */
          grid-row: footer-start / footer-end;
          grid-column: column-start 1 / grid-end;
      }
    ```

<h4 id='naminggridarea'>Naming Grid Area</h4>

-   Another option to name a grid, is to name the **area** using `grid-template-areas`

    ```CSS
      .container {
          width: 1000px;
          margin: 30px auto;
          display: grid;
          grid-template-rows: 100px 200px 400px 100px;
          grid-template-columns: repeat(3, 1fr) 200px;
          grid-gap: 30px;

          grid-template-areas:
              'header header header header'
              'box box box sidebar'
              'main main main sidebar'
              'footer footer footer footer';
      }

      .header {
          grid-area: header;
      }

      .main-content {
          grid-area: main;
      }

      .sidebar {
          grid-area: sidebar;
      }

      .footer {
          grid-area: footer;
      }
    ```

    -   if we don't want to place an empty cell, we can do so using `.`. **ATTENTION** make sure you have defined all the `grid-area` otherwise this not might work

<h4 id='implicitvsexplicit'>Implicit vs Explicit</h4>

-   `Explicit` means that we explicit specified the size of the grid
-   `Implicit` mean that we have more grids than we have specified

-   We can set some default values

    -   `grid-auto-rows`, defines the height of each row if not specified
    -   `grid-auto-columns`, defines the width of each column if not specified
    -   `grid-auto-flow: row | column;`, just like `display: flex;` the default value is `row`, this means that all the remaining (implicit) grids will grow as rows.
        -   This will change the display orientation too

    ```CSS
      .container {
          width: 1000px;
          margin: 38px auto;
          background-color: #ddd;

          display: grid;
          grid-template-rows: repeat(2, 150px);
          grid-template-columns: repeat(2, 1fr);
          grid-gap: 30px;

          grid-auto-rows: 80px;
          grid-auto-columns: 0.5fr;
          grid-auto-flow: column;
      }

      .item {
          padding: 20px;
          color: white;
          font-family: sans-serif;
          font-size: 30px;
          background-color: orangered;
      }
    ```

<h4 id='aligngriditems'>Align Grid Items</h4>

-   To align the items inside of a grid area, we can use `align-items` to align vertically and `justify-items` to align horizontally (we don't have justfy-items to **flexbox**).

    -   Just like in **flexbox** the default valeu of **align-items** is `stretch` and one we override this command, the item will shrink to occupies only the space that it needs

    ```CSS
      .container {
          width: 1000px;
          margin: 38px auto;
          background-color: #ddd;

          display: grid;
          grid-gap: 30px;

          grid-auto-rows: 80px;
          grid-auto-columns: 0.5fr;
          grid-auto-flow: row;

          /* Align grid tracks to grid container */
          height: 1000px;
          grid-template-rows: repeat(2, 100px);
          grid-template-columns: repeat(2, 200px);
          justify-content: center;
          align-content: center;
      }

      .item {
          padding: 20px;
          color: white;
          font-family: sans-serif;
          font-size: 30px;
          background-color: orangered;
      }

      .item--4 {
          grid-row: 2 / span 3;
          align-self: start;
          justify-self: start;
      }

      .item--7 {
          grid-column: 1 / -1;
          background-color: orchid;
      }
    ```

<h4 id='fixinggridholes'>Fixing Grid Holes</h4>

-   Sometimes we have some holes in our grid area, because the automatically placement cannot tries to keep the sequence of our code, instead it follows the sequence that we create on our css, and that might cause some holes in our grid
-   To fix that we can add the **dense** to our `grid-auto-flow`

<h4 id='maxcontent'>max-content</h4>

-   With `max-content` it will grow the size of the grid cell to accomodate the inner content

    ```CSS
      .container {
          width: 1000px;
          margin: 38px auto;
          background-color: #ddd;

          display: grid;
          grid-template-rows: repeat(2, 150px);
          grid-template-columns: max-content 1fr 1fr max-content;
      }

      .item {
          padding: 20px;
          color: white;
          font-family: sans-serif;
          font-size: 30px;
          background-color: orangered;
      }

      .item--1 {
          background-color: orangered;
      }

      .item--2 {
          background-color: yellowgreen;
      }

      .item--3 {
          background-color: blueviolet;
      }

      .item--4 {
          background-color: palevioletred;
      }

      .item--5 {
          background-color: royalblue;
      }

      .item--6 {
          background-color: goldenrod;
      }

      .item--7 {
          background-color: crimson;
      }

      .item--8 {
          background-color: darkslategray;
      }
    ```

<h4 id='mincontent'>min-content</h4>

-   With `min-content` it will grow until the min size that the grid needs to grow. In other words, it will grow up to the biggest single word width.

<h4 id='minmaxgrid'>minmax()</h4>

-   The `minmax()` uses the minimum space that the grid needs and uses the max-content to grow as much it needs to fit the content
    -   `grid-template-rows: repeat(2, minmax(150px, min-content));`
    -   `grid-template-columns: minmax(200px, 300px) repeat(3, 1fr);`

<h4 id='autofitautofill'>Auto-Fit and Auto-Fill</h4>

-   **Auto-Fill**

    -   `auto-fill` will automatically create the grid to fill the all the remaining space. In this case we have a width of `1000px` and we want to create a grid that has `100px`, so it will fill with `10 columns`

    ```CSS
      .container {
          width: 1000px;
          margin: 38px auto;
          background-color: #ddd;

          display: grid;
          grid-template-rows: repeat(2, minmax(150px, min-content));
          grid-template-columns: repeat(auto-fill, 100px);
      }
    ```

-   **Auto-Fit**

    -   `auto-fit` just like `auto-fill`, it will create `10 columns` but with the difference that it will colapse the unused grids leaving with an empty space

    ```CSS
      .container {
          width: 1000px;
          margin: 38px auto;
          background-color: #ddd;

          display: grid;
          grid-template-rows: repeat(2, minmax(150px, min-content));
          grid-template-columns: repeat(auto-fit, 100px);
      }
    ```

    -   One option woul be to use `auto-fit` with `min-max(200px, 1fr)`, and a width realtive to the viewport(in **%**). Just like `diplay: flex;`, `flex-wrap: wrap;` if we change the viewport the content (the grid) will adapt to use the min `200px` or max of `1fr`. If the content doesn't fit, it will move the item to the next line

    ```CSS
      .container {
          width: 90%;
          margin: 38px auto;
          background-color: #ddd;

          display: grid;
          grid-template-rows: repeat(2, minmax(150px, min-content));
          grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      }
    ```

<!-- // ~~> ANIMATION -->
<h2 id='animation'>Animation</h2>

<!-- // ~~~> @keyframes -->
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

<!-- // ~~~> Transition -->
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

<h4 id='multipletransitions'>Multiple Transitions</h4>

-   We could create cool animations using the `::before` pseudo element

    -   we can set differnt times for different properties

    ```SCSS
      transition: transform 0.2s,
                  width 0.4s cubic-bezier(1, 0, 0, 1) 0.2s,
                  background-color 0.1s;
    ```

    -   In this case we are the `transform 0.2s` this is responsible to change the `scaleY()` that initially is set to **0**, and then when we hover, it changes to `scaleY(1)` in `0.2s`
    -   the second property we have `width 0.4s cubic-bezier(1, 0, 0, 1) 0.2s` where we initially we have width of `3px`, then when we hover we change to **100%** in `0.4s` using the speed of `cubic-bezier` with a delay of `0.2s` before starting the animation
    -   for last we have `background-color 0.1s` where when we click, the the `::before` pseudo element, changes the color to brighter color in `0.1s`

    ```HTML
      <nav class="sidebar">
          <ul class="side-nav">
              <li class="side-nav__item side-nav__item--active">
                  <a href="#" class="side-nav__link">
                      <svg class="side-nav__icon">
                          <use xlink:href="img/sprite.svg#icon-home"></use>
                      </svg>
                      <span>Hotel</span>
                  </a>
              </li>
              <li class="side-nav__item">
                  <a href="#" class="side-nav__link">
                      <svg class="side-nav__icon">
                          <use xlink:href="img/sprite.svg#icon-aircraft-take-off"></use>
                      </svg>
                      <span>Flight</span>
                  </a>
              </li>
              <li class="side-nav__item">
                  <a href="#" class="side-nav__link">
                      <svg class="side-nav__icon">
                          <use xlink:href="img/sprite.svg#icon-home"></use>
                      </svg>
                      <span>Car Rental</span>
                  </a>
              </li>
              <li class="side-nav__item">
                  <a href="#" class="side-nav__link">
                      <svg class="side-nav__icon">
                          <use xlink:href="img/sprite.svg#icon-map"></use>
                      </svg>
                      <span>Tours</span>
                  </a>
              </li>
          </ul>
          <div class="legal">
              &copy; 2017 by trillo. All rights reserved.
          </div>
      </nav>
    ```

    ```SCSS
      .side-nav {
          font-size: 1.4rem;
          list-style: none;
          margin-top: 3.5rem;

          &__item {
              position: relative;

              &::before {
                  content: '';
                  position: absolute;
                  top: 0;
                  left: 0;
                  height: 100%;
                  background-color: var(--color-primary);
                  transform: scaleY(0);
                  width: 3px;
                  transition: transform 0.2s, width 0.4s cubic-bezier(1, 0, 0, 1) 0.2s,
                      background-color 0.1s;
              }
              &:not(:last-child) {
                  margin-bottom: 0.5rem;
              }
              &--active::before,
              &:hover::before {
                  transform: scaleY(1);
                  width: 100%;
              }
              &:active::before {
                  background-color: var(--color-primary-light);
              }
          }
          &__link {
              color: var(--color-grey-light-1);
              text-decoration: none;
              display: block;
              padding: 1.5rem 3rem;
              position: relative;
              z-index: 2;
          }
          &__icon {
              width: 1.75rem;
              height: 1.75rem;
              margin-right: 2rem;
              fill: currentColor;
          }
      }
    ```

    -   **OBS** the `z-index` only works if we have a `positon` set to the item

<h4 id='pseudoclasses'>Pseudo Classes</h4>

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

<h4 id='pseudoelements'>Pseudo Elements</h4>

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

<h4 id='chainingpsudeoclasses'>Chaining Pseudo Classes - Validation</h4>

[Go Back to Summary](#summary)

-   we can use chaining pseudo classes to to some form validations

    -   [placeholder](https://css-tricks.com/almanac/selectors/p/placeholder/)

    ```SCSS
      &__input {
          font-size: 1.5rem;
          font-family: inherit;
          color: inherit;
          padding: 1.5rem 2rem;
          border-radius: 0.2rem;
          background-color: rgba($color-white, 0.5);
          border: none;
          border-bottom: 0.3rem solid transparent;
          width: 40%;
          display: block;
          transition: all 0.3s;

          &:focus {
              outline: none;
              box-shadow: 0 1rem 2rem rgba($color-black, 0.1);
              border-bottom: 0.3rem solid $color-primary;
          }
          &:focus:invalid {
              border-bottom: 0.3rem solid $color-secondary-dark;
          }
          &::-webkit-input-placeholder {
              color: $color-grey-dark-2;
          }
          &:valid {
              border-bottom: 0.3rem solid $color-primary;
          }
          &:invalid {
              border-bottom: 0.3rem solid $color-secondary-dark;
          }
      }
    ```

<h4 id='cubicbezier'>Cubic-Bezier</h4>

-   [Cubic-Bezier Graphic](https://easings.net/)
-   [Cubic-Bezier Vizualization](https://cubic-bezier.com/#.17,.67,.83,.67)
-   The `cubic-bezier()` function defines a Cubic Bezier curve.
-   A Cubic Bezier curve is defined by four points P0, P1, P2, and P3. P0 and P3 are the start and the end of the curve and, in CSS these points are fixed as the coordinates are ratios. P0 is (0, 0) and represents the initial time and the initial state, P3 is (1, 1) and represents the final time and the final state.
-   The `cubic-bezier()` function can be used with the animation-timing-function property and the transition-timing-function property.

    ```CSS
      cubic-bezier(x1,y1,x2,y2)
    ```

<!-- // ~~~> Advanced Hover -->
<h3 id='advancedhover'>Advanced Hover</h3>

[Go Back to Summary](#summary)

```SCSS
  .composition {
      position: relative;

      &__photo {
          width: 55%;
          box-shadow: 0 1.5rem 4rem rgba($color-black, 0.4);
          border-radius: 0.2rem;
          position: absolute;
          z-index: 10;
          outline-offset: 2rem;
          transition: all 0.2s;

          &--p1 {
              left: 0;
              top: -2rem;
          }
          &--p2 {
              right: 0;
              top: 2rem;
          }
          &--p3 {
              left: 20%;
              top: 10rem;
          }
          &:hover {
              transform: scale(1.05) translateY(-0.5rem);
              box-shadow: 0 2rem 4rem rgba($color-black, 0.5);
              z-index: 20;
              outline: 1.5rem solid $color-primary;
          }
      }
      &:hover &__photo:not(:hover) {
          transform: scale(0.95) translateY(0.5rem);
      }
  }
```

<h4 id='hoverselectingmodifier'>Hover Selecting Modifiers</h4>

```SCSS
  &:hover &__photo:not(:hover) {
      transform: scale(0.95);
  }
```

-   in this case we are:
    -   when `div` is `hovered`
    -   then select the `composition__photo`
    -   then with the the `elements that are not hovered` scale down to `95%`

<!-- // ~~~> Rotating -->
<h3 id='rotating'>Rotating</h3>

[Go Back to Summary](#summary)

-   To rotate an element, we can simply call transform do to so, but the effect it's not that great.
-   It's hard to distinguish what is rotating

    ```SCSS
      .card {
          &:hover {
              transform: rotateY(180deg);
          }
      }
    ```

-   the final result we will have:

    ```HTML
      <div class="card">
          <div class="card__side card__side--front">
              FRONT
          </div>
          <div class="card__side card__side--back card__side--back-1">
              BACK
          </div>
      </div>
    ```

    ```SCSS
      .card {
          perspective: 150rem;
          -moz-perspective: 150rem;
          position: relative;
          height: 50rem;

          &__side {
              height: 50rem;
              transition: all 0.8s ease;
              position: absolute;
              top: 0;
              left: 0;
              width: 100%;
              backface-visibility: hidden;
              border-radius: 0.3rem;
              box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

              &--front {
                  background-color: $color-white;
              }
              &--back {
                  transform: rotateY(-180deg);

                  &-1 {
                      background-image: linear-gradient(
                          to right bottom,
                          $color-secondary-light,
                          $color-secondary-dark
                      );
                  }
              }
          }
          &:hover &__side--front {
              transform: rotateY(180deg);
          }
          &:hover &__side--back {
              transform: rotateY(0);
          }
      }
    ```

<h4 id='perspective'>Perspective</h4>

-   Adding a **perspective** helps us to visualize what is rotating
-   We added the `-moz-perspective` to make it work in mozilla firefox
-   The **perspective** always have to be declared on the parent element
-   Then we create the element that we want to rotate
    ```SCSS
      &__side {
          background-color: orangered;
          height: 50rem;
          transition: all 0.8s;
      }
    ```
-   After that we create the condition

    ```SCSS
      &:hover &__side {
          transform: rotateY(180deg);
      }
    ```

    -   In this case, when we **hover** the `card` element, then the `__side` element will transform (rotate 180 degrees on the Y axis)

    ```SCSS
      .card {
          perspective: 150rem;
          -moz-perspective: 150rem;

          &__side {
              background-color: orangered;
              height: 50rem;
              transition: all 0.8s;
          }
          &:hover &__side {
              transform: rotateY(180deg);
          }
      }
    ```

<h4 id='backfacevisibility'>Backface-visibility</h4>

-   the `backface-visibility` property hides the back of the element, in the case we are rotating an element, we can see the text rotated as well
-   To the back card be in the back of the front card, we need to define `position: relative;` to the parent element
    -   and because we gave the parent a **relative position** and the child an **absolute position**. the element loses their height, that's why we need to give the same height of the child element to the parent element, otherwise, the element will have only the necessary height
-   To finish our element, we just need to update the hover condition

    -   when the card is loaded
        -   the front of the card is normal (not rotated)
        -   the back of the card is rotated 180 degrees
    -   when we hover the card
        -   the front of the card is rotated -180 degrees
            -   the `-` minus, it's just to give the impression that the card rotated 180 degrees completed
        -   the back of the card is back to normal (not rotated)

    ```SCSS
      .card {
          perspective: 150rem;
          -moz-perspective: 150rem;
          position: relative;
          height: 50rem;

          &__side {
              height: 50rem;
              transition: all 0.8s ease;
              position: absolute;
              top: 0;
              left: 0;
              width: 100%;
              backface-visibility: hidden;
              border-radius: 0.3rem;
              box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

              &--front {
                  background-color: $color-white;
              }
              &--back {
                  transform: rotateY(-180deg);

                  &-1 {
                      background-image: linear-gradient(
                          to right bottom,
                          $color-secondary-light,
                          $color-secondary-dark
                      );
                  }
              }
          }
          &:hover &__side--front {
              transform: rotateY(180deg);
          }
          &:hover &__side--back {
              transform: rotateY(0);
          }
      }
    ```

<!-- // ~~> POPUP -->
<h2 id='popup'>Popup</h2>

[Go Back to Summary](#summary)

-   creating our popup coainter that will have the entire screen

    ```HTML
      <div class="popup" id="popup">
          <div class="popup__content">
              <div class="popup__left">
                  <img src="img/nat-8.jpg" alt="Tour photo" class="popup__img">
                  <img src="img/nat-9.jpg" alt="Tour photo" class="popup__img">
              </div>
              <div class="popup__right">
                  <a href="#section-tours" class="popup__close">&times;</a>
                  <h2 class="heading-secondary u-margin-bottom-small">Start booking now</h2>
                  <h3 class="heading-tertiary u-margin-bottom-small">Important&ndash; Please read these terms before
                      booking</h3>
                  <p class="popup__text">
                      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore
                      et dolore magna aliqua. Nunc congue nisi vitae suscipit tellus mauris a. Sagittis orci a scelerisque
                      purus semper
                      eget duis at. Lorem ipsum dolor sit amet consectetur adipiscing elit ut aliquam. Morbi blandit
                      cursus risus at ultrices.
                      In est ante in nibh mauris. Suspendisse interdum consectetur libero id faucibus nisl tincidunt. Mi
                      tempus imperdiet
                      nulla malesuada pellentesque elit eget gravida cum. Pellentesque pulvinar pellentesque habitant
                      morbi tristique
                      senectus et netus. Et netus et malesuada fames ac turpis egestas maecenas. Odio facilisis mauris sit
                      amet massa vitae
                      tortor condimentum. Turpis massa sed elementum tempus.
                  </p>
                  <a href="#" class="btn btn--green">Book now</a>
              </div>
          </div>
      </div>
    ```

    ```SCSS
      .popup {
          width: 100vw;
          height: 100%;
          position: fixed;
          top: 0;
          left: 0;
          background-color: rgba($color-black, 0.8);
          z-index: 300;
          transition: all 0.3s;
          opacity: 0;
          visibility: hidden;

          &__content {
              @include center-abs-horizontal-vertical;
              width: 75%;
              box-shadow: 0 2rem 4rem rgba($color-black, 0.2);
              background-color: $color-white;
              border-radius: 0.3rem;
              overflow: hidden;
              display: flex;
              transition: all 0.4s 0.2s;
              transform: translate(-50%, -50%) scale(0.5);
              opacity: 0;
          }
          &__left {
              width: 33.3333%;
              display: flex;
              flex-direction: column;
          }
          &__right {
              width: 66.6666%;
              margin: auto 0;
              padding: 3rem 5rem;
          }
          &__img {
              display: block;
              width: 100%;
          }
          &__text {
              font-size: 1.4rem;
              margin-bottom: 4rem;
              -moz-column-count: 2;
              -moz-column-gap: 4rem;
              -moz-column-rule: 1px solid $color-grey-light-2;
              column-count: 2;
              column-gap: 4rem;
              column-rule: 1px solid $color-grey-light-2;
              -moz-hyphens: auto;
              -ms-hyphens: auto;
              -webkit-hyphens: auto;
              hyphens: auto;
          }
          &:target {
              opacity: 1;
              visibility: visible;
          }
          &:target &__content {
              transform: translate(-50%, -50%) scale(1);
              opacity: 1;
          }
          &__close {
              position: absolute;
              top: 2.5rem;
              right: 2.5rem;
              font-size: 3rem;
              text-decoration: none;
              display: inline-block;
              transition: all 0.2s;
              line-height: 1;

              &:hover {
                  color: $color-primary;
              }
          }
      }
    ```

<!-- // ~~~> Target -->
<h3 id='target'>Target</h3>

[Go Back to Summary](#summary)

-   in CSS we have a `:target` pseudo class, that activates when the element is on focus using the anchor tag `<a href="#popup">`

<!-- // ~> BEM (Block Element Modifier) -->
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

<!-- // ~> SASS -->
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

<!-- // ~~> SASS VARIABLE -->
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

<!-- // ~~> SASS MIXIN -->
<h2 id='sassmixin'>Sass Mixin</h2>

[Go Back to Summary](#summary)

-   A `Mixin` is like a function, we can pass arguments, the only difference is that a `mixin` doesn't return anything, it only applies the style

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

<!-- // ~~~> Calling a Mixin -->
<h3 id='usingmixin'>Calling a Mixin</h3>

[Go Back to Summary](#summary)

-   To call a `mixin` we just need to **@include** `<name-of-the-mixin>`
-   With a `mixin` we can pass arguments

    ```SCSS
      a {
          @include style-text-light ($color-text-dark);
      }
    ```

-   Another thing that we can do with `mixin`, instead of passing an argument, we can pass a block of styles using **@content**
-   So use the block of content we need to declare the mixing using the following boilerplate

    ```SCSS
      @mixin media-query-phone {
          @media (max-with: 600px) {
              @content
          }
      }
    ```

-   And when we call the `mixin`

    ```SCSS
      html {
          @include media-query-phone {
              font-size: 50%;
          }
      }
    ```

<!-- // ~~> SASS FUNCTIONS -->
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

<!-- // ~~> SASS EXTEND -->
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

// ~~> SASS PARTIALS

<h2 id='sasspartials'>Sass Partials</h2>

[Go Back to Summary](#summary)

-   **Partials** are SCSS files that we split across our project
-   We declare as `_name.scss`

<!-- // ~~~> Immport Partials -->
<h3 id='sassimportpartial'>Import Partials</h3>

[Go Back to Summary](#summary)

-   To import a partial we just need to use the `@import` and then specify the path to the file `@import 'base/base';`
-   Notice that we didn't need to add `_` before base and the extension. Sass compiler understands that we want to import the `_base.scss`

<!-- // ~> RESPONSIVE WEB DESIGN -->
<h1 id='responsivedesign'>Responsive Web Design</h1>

<!-- // ~~> Mobile First -->
<h2 id='mobilefirst'>Mobile First</h2>

[Go Back to Summary](#summary)

-   Start writing CSS for mobile devices: small screen;
-   Then, media queries expand design to a large desktop screen
-   Forces us to reduce websites and apps to the absolute essentials

    ```SCSS
      html {
          font-size: 16px
      }

      @media(min-width: 600px) {
          html {
            font-size: 20px;
          }
      }
    ```

<!-- // ~~> Media Queries Sizes -->
<h2 id='mediaqueriessizes'>Media Queries Sizes</h2>

[Go Back to Summary](#summary)

-   `0 - 600px` phone
-   `600 - 900px` tablet portrait
-   `900 - 1200px` tablet landscape
-   `1200 - 1800px` is where our nomal css apply
-   `1800px +` big desktop

-   **Mobile first** approach

    ```Bash
        |------------------|------------------|------------------|------------------>
        0px               600px              900px             1200px               infinity

                          |-------------------------------------------------------->|
                            min-width: 600px;
                            isWidth >= 600px ?
                                              |------------------------------------->|
                                                min-width: 900px;
                                                isWidth >= 900px ?
                                                        |--------------------------->|
                                                          min-width: 1200px;
                                                          isWidth >= 1200px ?

          Minimum width at which media query still applies
    ```

-   **Desktop first** approach

    ```Bash
        |------------------|------------------|------------------|------------------>
        0px               600px              900px             1200px               infinity

        |----------------->|
          max-width: 600px;
          isWidth <= 600px ?
        |------------------------------------>|
                            max-width: 900px;
                            isWidth <= 900px ?
        |------------------------------------------------------->|
                                              max-width: 1200px;
                                              isWidth <= 1200px ?

          Maximum width at which media query still applies
    ```

<!-- // ~~~> Media Query With SASS -->
<h2 id='mediaquerysass'>Media Query With SASS</h2>

[Go Back to Summary](#summary)

-   to help with our media query, we can can create `mixin` to handle different screens sizes, and also have a centralized configuration file
-   a good way to manage all the possible media query configurations, is to create a media query manager using `mixin`

    -   we can create different breakpoints, to do so we need to use the `@if` statement

-   To make our website responsive, we need to use `em` instead of `pixels`

    -   We are using `em` bacuase `rem` doesn't work properly in all the browsers
    -   `1em` equals to **16px**

    |   em    |   px   |
    | :-----: | :----: |
    | 37.5em  | 600px  |
    | 56.25em | 900px  |
    |  75em   | 1200px |
    | 112.5em | 1800px |

-   in `_mixin.scss`

    ```SCSS
      /*
          = MEDIA QUERY BREAKPOINS
          + phone
          + tab-port
          + tab-land
          + big-desk
      */

      @mixin mq-manager($breakpoint) {
          @if $breakpoint == phone {
              @media (max-width: 37.5em) {
                  // 600px
                  @content;
              }
          }
          @if $breakpoint == tab-port {
              @media (max-width: 56.25em) {
                  // 900px
                  @content;
              }
          }
          @if $breakpoint == tab-land {
              @media (max-width: 75em) {
                  // 1200px
                  @content;
              }
          }
          @if $breakpoint == big-desk {
              @media (max-width: 112.5em) {
                  // 1800px
                  @content;
              }
          }
      }
    ```

-   in `_base.scss`

    ```SCSS
      html {
          font-size: 62.5%; // 1rem = 10px; 10px/16px = 62.5%

          @include mq-manager(big-desk) {
              // width < 1800px ?
              font-size: 75%; // 1rem = 12px, 12/16 = 75%
          }
          @include mq-manager(tab-land) {
              // width < 1200px ?
              font-size: 56.25%; // 1rem = 9px, 9/16 = 56.25%
          }
          @include mq-manager(tab-port) {
              // width < 900px ?
              font-size: 50%; // 1rem = 8px, 8/16 = 50%
          }
          @include mq-manager(phone) {
              // width < 600px ?
              font-size: 30%; // 1rem = 4.8px, 4.8/16 = 30%
          }
      }
    ```
