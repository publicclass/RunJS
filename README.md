# RunJS

A simple lightweight library to run the appropriate scripts depending on a pathname or selector.


## Usage

    // Run when pathname ends with /slideshow
    // the splatted part (the '*all'-part) is passed on
    // as an argument along with the complete url
    $.run("/*all/slideshow",function(all,url){
      $(".slideshow").load(all)
    })
    
    // Run when a selector is matched on the page
    $.run(".pagination",function(){
      // `this` will be the same as if it was called through $(".pagination")
    })
    
    // Basically the same as $(), but here for completeness
    $.run(function(){
      
    })

    // Also add them all at once by passing an object
    $.run({
      // Run these when the url ends with /slideshow
      "/*all/slideshow": function(all,url){},
      
      // Run this on url '/press'
      "/press": function(url){},
      
      // Run this if '.pagination' selector is found
      ".pagination": function(){}
    })


## Features

* Run scripts based on a pathname or a css selector

* The _pathname_ should be parsed from either (in this order)
  
  1. a hashbang (i.e. a window.location.hash starting with #!)
  2. address bar (i.e. the window.location.pathname)

* Run the script again (in case anything has updated)

        window.addEventListener("onhashchange",function(){
          // Run all (currently matching) routes again
          $.run()
          
          // Run only a particular one
          $.run("/*all/slideshow")
        })


## TODO

By the big `1.0` we should also have a few extra features like:

* Adapters for hashchange and push/pop-State that runs, ehm, `$.run()` whenever it has changed
* Work just as well without jQuery (i.e. be framework agnostic) and only support selectors if a selector engine is available (like Sizzle or document.querySelectorAll)
* Allow loading of external scripts depending on route (if Modernizr is available) before the callback is called (i.e. it'll be the 'complete'-callback instead)
* Maybe be able to name the routes so it'll be more convenient to rerun a particular route
* Maybe return the matched wildcards in the route of a pathname in a params-hash instead