---
title: Snakes on a Page
cover-image: 
tags: [projects]
---

Press **s**. 
Press **Down Arrow**.
Press **Right Arrow**.

Congratulations, if you are not on a phone, you just played the game Snake on this page.

It is an adaption of this [Codepen Snake game][snake] to overlay the webpage. My particular implementation is having a *snake.js* file generate the snake code into a `<canvas>` element. The `<canvas>` element is initially set to `display:none;` such that it does not show up until the user presses 's'. Then *snake.js* runs the game, which overlays the content of the page. 

You can find the [snake.js code here](https://github.com/rebeccali/holo-alfa/blob/master/js/snake.js). 

## Adding Snake to your own webpage ##

To add snake to your own webpage, do the following: 

1. Insert the `<canvas>` tag nested within the `<body>`. This is where the snake graphics box will live. Don't worry about the height and width, they are set to dummy values for now. Skip to step 4 to see how to change these values when the game is initialized.


    {% highlight HTML %}
     <body>
        <canvas class="snake" id="stage" height="400" width="520" style="display:none;"></canvas>
        <div class="wrap" id="wrap1">
            ...
        </div>
    </body>
    {% endhighlight %}

2. Then, save the [*snake.js*](https://github.com/rebeccali/holo-alfa/blob/master/js/snake.js) file to somewhere in your website directory. In the `<head>` tag, add the link to your *snake.js*.

    <head>
        <script src="/js/snake.js"></script>
    </head>

3. In your webpage's main style sheet (.css), add in the following CSS, which allows snake to float over your content:
    {% highlight css %}
      canvas.snake {
        position: fixed;
        margin: 0 auto;
        left: 0;
        right:0;
      }
    {% endhighlight %}

4. Now, maybe we want to adjust the height and width of the snake game. In that case, within *snake.js* there is a `Game.Snake = function(elementId, conf)` funciton, whose implementation is below. Change the `var wrap1` to the element of your choice, such that snake matches the height and width of that element. Alternatively, omit `var wrap1 = ...` and the two following lines to let the canvas stay the size initialy determined by the HTML in step 1. 
  {% highlight javascript %}
    Game.Snake = function(elementId, conf) {
      
      // Sets the game size
      var canvas   = document.getElementById(elementId);
      var wrap1 = document.getElementsByTagName("body")[0];
      canvas.width = wrap1.offsetWidth - 1;
      canvas.height = wrap1.offsetHeight - 1;
      var context  = canvas.getContext("2d");
      var snake    = new Component.Snake(canvas, conf);
      var gameDraw = new Game.Draw(context, snake);
      
      // Game Interval
      setInterval(function() {gameDraw.drawStage();}, snake.stage.conf.fps);
    };
  {% endhighlight %}

There you go! Leave a comment if you have any issues. Also now I have syntax highlighting! 




[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[githubpages]: https://pages.github.com/
[mywebsite]:   https://github.com/rebeccali/holo-alfa/
[holoalfa]:    https://github.com/steinvc/holo-alfa
[ppprs]:       http://www.powerracingseries.org/
[dvr]:         http://www.ti.com/product/drv8302
[chainsawfet]: http://www.nxp.com/documents/data_sheet/PSMN7R0-100PS.pdf
[bayley]:      http://isopack.blogspot.com
[ninephase]:   https://github.com/rebeccali/ninephase
[openscad]:    http://www.openscad.org/
[geb]:         https://books.google.com/books/about/G%C3%B6del_Escher_Bach_Anniversary_Edition.html?id=aFcsnUEewLkC&source=kp_cover
[openscadrepo]:https://github.com/rebeccali/openscad
[snake]:       http://codepen.io/CaioPaiola/pen/GFpuK
