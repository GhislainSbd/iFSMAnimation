iFSMAnimation
=============

Create simple HTML5 animations in responsive design easily and quickly, writing only one line of javascript code!

You describe the DOM objects that you want to animate, attached them to the animation machine, and let's animate!

To use it, have a look on the examples provided...

What is iFSMAnimation ?
=======================

iFSMAnimation is javascript library that allows to create animations from an html description.

Getting started
===============

Mainly, you need to create:
* a HTML 'section' (or whatever) that will define where is defined the animation and HTML 'articles' to define the different objects that must be animated.
* at the end, add a little script to start the animation... 
* that's it! You've got an animation that is RESPONSIVE ! Without having to know how to write javascript code lines...

```html
<section id="animation-objects" data-delay-before-restart="3000">
        <article id="HappyNewYear_B" data-animation="animate,300,168,220" data-enter-animation="display, 200, 90, 104, 90, 104" data-exit-animation="smoothHide,100,90,104">
        	<img src="images/B.png">
        </article>
        <article id="HappyNewYear_O" data-animation="specialAnimate,300,{left:500;top:130;width:250}" data-enter-animation="display,200,170,104,170,104" data-exit-animation="smoothHide,100,170,104">
        	<img src="images/O.png">
        </article>
                <article id="HappyNewYear_star" data-animation="rotate,20000,3060" data-enter-animation="display,10,277,417,277,417" data-exit-animation="smoothHide,100,433,-220">
        	<img src="images/etoile.png">
        </article>
        <article id="HappyNewYear_N3" data-animation="dummy" data-enter-animation="display,200,252,104,252,104" data-exit-animation="smoothHide,100,252,104">
        	<img src="images/N.png">
        </article>        
</section>
<script>
$(document).ready(function() {
	//wait for the download of the images if any...
	$('#animation-objects').waitForImages().done(function() {
		//initialize and start the general animation
		$('#animation-objects').iFSM(mainAnimation);
	});
)};
</script>
```

General process
===============

An animation is defined by a main animation object attached to a container such a 'section'.

Within the container, you define the different animated objects attached/described by a subcontainer that is by default an 'article'. 

Take care to **give an id to each object you will animate**.

The animation starts by calling each animated objects using the 'data-enter-animation' and just after 'data-animation' attributes to animate them.

When all objects were animated, the animation applies the 'data-exit-animation' definition of every animated objects to ending their animations, and then loops back.

Attributes on the main container
===============================
data-delay-before-restart
-------------------------
The 'data-delay-before-restart' attribute allows to define the delay before the animation restarts. 

Example: 
```html
<section id="animation-objects" data-delay-before-restart="10000">
```

data-box-responsive
-------------------
Boolean, if 'true', the animation will be 'responsive'.
Limitations known with using 'specialAnimate'.

Example: 
```html
<section id="animation-objects" data-box-responsive="true">
```


data-box-size-reference
-----------------------

"BoxWidth,BoxHeight" give the used dimensions as reference for the position of the animated objects. Useful in Responsive mode.

Example: 
```html
<section id="animation-objects" data-box-size-reference="551,551" >
```

data-keep-height-visible
------------------------
Boolean, if 'true', the width and height will be fixed in order that the animation is fully shown on the window display.
Example: 
```html
<section id="animation-objects" data-keep-height-visible="true">
```
 

data-div-class
--------------
Actually, a 'div' encapsultes the animation. It is possible to define the class that should be used on this div.

Example: 
```html
<section id="animation-objects" data-div-class="animation">
```

data-loader-class
-----------------

A loader may be set during initialization. 

To display a loader, just indicate the class to use with the data-loader-class attribute.

Example: 
```html
<section id="animation-objects" data-loader-class="myLoaderClass">
```

 
Attributes on a sub container
=============================

data-enter-animation / data-animation / data-exit-animation
-----------------------------------------------------------
  
  These attributes define the animation of the object.
  
  The available animation are:
   * dummy - non animation
   * animate - animate article from current position or startposition to destination
     *  duration
     *  destination-left
     *  destination-top
     *  startposition-left - optional
     *  startposition-top - optional
   * animateNoWait - same as animate but does not wait the end of animation to start the next animation 
   * display - display article (opacity set to 1) with animation from current position or startposition to destination
     *  duration
     *  destination-left
     *  destination-top
     *  startposition-left - optional
     *  startposition-top - optional
   * smoothHide - display article (opacity set to 0) with animation from current position or startposition to destination
     *  duration
     *  destination-left
     *  destination-top
     *  startposition-left - optional
     *  startposition-top - optional
   * rotate - rotate article 
     *  duration
     *  angle
   * loop - loop animation
     *  duration
     *  destination-left
     *  destination-top
     *  startposition-left - optional
     *  startposition-top - optional
     *  loops number - optional default:infinite - give the number of loops
     *  loop back delay - optional default: duration - give the delay to go to the initial position
   * specialAnimate
     *  duration
     *  animation description object as in jQuery. ex: {left: 20;top:100;width:300}

Start the animation with javascript
===================================
To start the animation, you will need to add this script:
```javascript
<script>
$(document).ready(function() {
	//initialize and start the general animation
	$('section').iFSM(mainAnimation);
)};
</script>
```

You can define some options on the iFSM machine:
animationSequence
-----------------
array, defines the order of animation of the objects. By default, the order is the one found in the DOM.

animatedObjectDefinition
------------------------
string, gives the HTML tag to find the animated objects (in css/jquery format).

examples:
---------
```javascript
var myAnimationSequence=['#myAnimObj2','#myAnimObj1'];
$('#animation-objects').iFSM(mainAnimation,{animationSequence:myAnimationSequence})
$('#animation2').iFSM(mainAnimation,{animatedObjectDefinition:'div',debug:true});
```


CCS
===

In order to have the animation playing correctly, you can use the following css as a start:

```css
body {
	margin		: 0px; 
	padding		: 0px;
	text-align	: center;
	}
/*for the div that embeds your animation section, will center it*/
#animation, .animation {
	margin : 0 20% 30px 20%;
}
/*for the main animation section container, let's have a background*/
#animation-objects,.animated_section {
	background-color:	#1c3970;
}
/*for the animated objects (here, all objects will start as hidden at beginning - opacity=0)*/
section#animation-objects article {
	opacity		: 0;
}
```

DEMO
====

http://intersel.net/demos/intersel/voeux_demo/

Examples
========

The 'examples' folder gives you some examples on how to animate your DOM objects with iFSMAnimation...

LIBRARY DEPENDENCIES
====================
To work properly, you need to include the following javascript library:
* jQuery (>= 1.10) `<script type="text/javascript" src="extlib/jquery-1.10.2.min.js"></script>`
* [iFSM by intersel](https://github.com/intersel/iFSM/)
  * this library manages finite state machines and needs these libraries:
    * doTimeout by ["Cowboy" Ben Alman](http://benalman.com/projects/jquery-dotimeout-plugin/)
	  * this library brings some very usefull feature on the usual javascript setTimeout function like Debouncing, Delays & Polling Loops, Hover Intent...
	  * `<script type="text/javascript" src="extlib/jquery.dotimeout.js"></script>`
    * attrchange by Selvakumar Arumugam](http://meetselva.github.io/attrchange/) 
	  * a simple jQuery function to bind a listener function to any HTML element on attribute change
	  * `<script type="text/javascript" src="extlib/jquery.attrchange.js"></script>`
* [waitForImages](http://github.com/alexanderdickson/waitForImages/) by Alexander Dickson, in order to garantee that all images of the animation are downloaded and ready. This library is automatically loaded by iFSMAnimation. You can change the used URL by setting yours in the ANIMATION_NEEDED_SCRIPTS[WAITFORIMAGES_ULR] global variable.

If you need to do some specific animations, these libraries may be useful:
  * [jquery.path](https://github.com/weepy/jquery.path) - allows to animate objects following a path as an arc or a curve 

FAQ
===

If you have questions or unsolved problems, you can have a look on the our [FAQs](https://github.com/intersel/iFSMAnimation/wiki) 
or leave a message on the [Issue board](https://github.com/intersel/iFSMAnimation/issues).


Contact
=======
If you have any ideas, feedback, requests or bug reports, you can reach me at github@intersel.org, 
or via my website: http://www.intersel.fr