```
Element.prototype.fixed = (function() {
        var x = 0,
          y = 0;
        return function(x1, y1) {
          var ele = this;
          ele.style.position = 'absolute';
          window.onscroll = function(e) {
            x = window.pageXOffset;
            y = window.pageYOffset;
            ele.style.left = x1 + x + 'px';
            ele.style.top = y1 + y + 'px';
          }
          ele.style.left = x1 + x + 'px';
          ele.style.top = y1 + y + 'px';
        }
      })();
      div.fixed(500, 400);
```