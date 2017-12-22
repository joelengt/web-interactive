# web-interactive
interactive web with custom query and scroll move to

```js

/* get query */
function getQueryByName(name, url) {
  if (!url) url = window.location.href;
  name = name.replace(/[\[\]]/g, "\\$&");
  var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"),
      results = regex.exec(url);
  if (!results) return null;
  if (!results[2]) return '';
  return decodeURIComponent(results[2].replace(/\+/g, " "));
}

/* Scroll move to a div-element */
(function($) {
    $.fn.goTo = function() {
        $('html, body').animate({
            scrollTop: $(this).offset().top + 'px'
        }, 'fast');
        return this; // for chaining...
    }
})(jQuery);

/* Custom url */
$( window ).on( "load", function() {
  var currentURL = window.location.url
  var currentView = getQueryByName('view', currentURL)

  /* evaluate custom url */
  switch(currentView) {
    case 'forgot-password':
      $('.btn__cambiar__contrasenia').click()
      $('.ctn__check__bloq').goTo()
      break;
  }

})

```




/* scroll event */

```js


/* SOLUTION 1*/

/* Scroll to a position ==> */
function scrollTo(position) {
  jQuery('.place-tiendas').animate({
    scrollTop: position + 'px'
  }, 'fast');
}


/* calc the element position in the block element */
jQuery('.go-to-place').click(function() {
  var self = this
  
  /* close the items */
  setTimeout(function(){
    // jQuery(self).find('.details').css('overflow', 'visible')
    // jQuery(self).find('.details').css('display', 'none')
    scrollTo(0)
  }, 1500)

  /* Get the element current top position */
  setTimeout(function() {
    var Tohere = jQuery(self).position().top
    console.log('element POSITION 2 =>', Tohere)
    scrollTo(Tohere)
    // jQuery(self).find('.details').css('display', 'block')
  }, 2000)

})





/* SOLUTION 2 */
function scrollTo(position) {
  jQuery('.place-tiendas').animate({
    scrollTop: position + 'px'
  }, 'fast');
}


/* calc the element position in the block element */
jQuery('.go-to-place').click(function() {
  var self = this

  setTimeout(function(){
    // scrollTo(0)
    var childPos = jQuery(self).position();
    var parentBoxScroll = jQuery('.place-tiendas').scrollTop();

    console.log('Child position, ', childPos)
    console.log('parent position, ', parentBoxScroll)

    var goTo = parentBoxScroll + (childPos.top)
    scrollTo(goTo)
  }, 1500)

})


```
