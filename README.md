# web-interactive
interactive web with custom query and scroll move to

´´´js

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

´´´
