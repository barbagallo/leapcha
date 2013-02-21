#Leapcha = Captcha + jQuery + Leap Motion
A proof of concept captcha-like jQuery plugin for use with the Leap Motion device/library.

## How It Works
* Manually disable your form, by emptying the form's `action` attribute, and placing its value in a hidden `<input>` with a specific ID. You need to also add `disabled="disabled"` on the submit button.
* Add the needed scripts to your page.
* Add a few HTML lines to your form to init Leapcha.
* The user draws the shape in the air and if it validates, the plugin inserts the form's `action` into the `<form>` tag. At this point the user is able to submit the form.

## How To Use

_NOTE: Below are steps that will get the index.html example working properly. You might need to tweak the process according to your current build configuration._

1. Include the libraries on the page:

	<script src="js/leap.js"></script>
	<script src="js/jquery-1.9.1.min.js"></script>
	<script src="js/bootstrap.min.js"></script>
	<script src="js/jquery.leapcha.1.0.js"></script>

	<link rel="stylesheet" href="css/bootstrap.css" media="screen" />
	<link rel="stylesheet" href="css/leapcha.css" />

2. Open a form element. You may add a unique ID (eg. '#contact-form') and set the form action to blank, e.g.:

        <form action="#" id="contact-form" method="GET or POST">

3. Add this `<canvas>` element to your form (you may use `<fieldset>` elements if you need it to validate/position). This is where the Leap output will show up:

            <canvas id="lc-canvas">
                Your browser doesn't support the canvas element - please visit in a modern browser.
            </canvas>

4. Disable the submit button, e.g.:

        <input type="submit" id="send-info" disabled="disabled" value="Submit Form" />

5. Add a hidden input to the form, with the form action as its value. Give it either a unique id, or the id 'lc-action', like so:

        <input type="hidden" id="send-info" value="submitform.php" />

6. Call the plugin on the form element. If you used any other ID than 'mc-action' for the hidden input, you'll just need to pass it to the plugin, like this:

        $('#contact-form').leapcha({
            action: '#send-info'
        });

        // Or, if you just used 'mc-action' as the hidden input's ID:
        $('#contact-form').leapcha();

7. Other options are available (defaults are shown):

        $('#contact-form').leapcha({
            // Basics:
            action: '#lc-action',        // the ID of the input containing the form action
            divId: '#lc-canvas',                // if you use an ID other than '#lc-canvas' for the placeholder, pass it in here
            cssClass: '.lc-active',      // this CSS class is applied to the 'lc-canvas' div when the plugin is active
            canvasId: '#lc-canvas',      // the ID of the Leapcha canvas element
            submitId: false,      // If your form has multiple submit buttons, give the ID of the one you'd like "activated" upon correct leapcha

            // An array of shape names that you want Leapcha to use:
            shapes: ['triangle', 'x', 'rectangle', 'circle', 'check', 'caret', 'zigzag', 'arrow', 'leftbracket', 'rightbracket', 'v', 'delete', 'star', 'pigtail'],

            // Canvas vars:
            canvasFont: '15px "Lucida Grande"',
            canvasTextColor: '#111',

            // These messages are displayed inside the canvas after a user finishes drawing:
            errorMsg: 'Please try again.',
            successMsg: 'Leapcha passed!',

            // This message is displayed if the user's browser doesn't support canvas:
            noCanvasMsg: "Your browser doesn't support <canvas> - try Chrome, FF4, Safari or IE9."

            // This could be any HTML string (eg. '<label>Draw the shape:</label>'):
            label: '<p>Please draw the shape in the box to submit the form:</p>',

            // Callback function to execute when a user successfully draws the shape
            // Passed in the form, the canvas and the canvas context
            // Scope (this) is active plugin options object (opts)
            // The default onSuccess callback function enables the submit button, and adds the form action attribute:
            onSuccess: function($form, $canvas, ctx) {
            	var opts = this,
	            $submit = opts.submitId ? $form.find(opts.submitId) : $form.find('input[type=submit]:disabled');

	            // Set the form action:
	            $form.attr( 'action', $(opts.actionId).val() );
			
	            // Enable the submit button:
	            $submit.prop('disabled', false);
			
	            return;
            },
		
            // Callback function to execute when a user successfully draws the shape
            // Passed in the form, the canvas and the canvas context
            // Scope (this) is active plugin options object (opts)
            onError: function($form, $canvas, ctx) {
	            var opts = this;
	            return;
            }
        });

## Technology

####Leap Motion
Leap Motion is unreleased to the consumer market (as of writing this README). It is slated to be sold in Bestbuy beginning Spring 2013. To read up more on how Leap Motion works and what it is, check out their [website](http://www.leapmotion.com/).

This project is a simple POC/example of how to use Leap Motion in the browser. You need the device in order to use this plugin.

## Quick Roadmap

### v1.1
* please start branching and helping out!

## Changelog

### v1.0
* Initial build.

## Credits
*Some parts of this project are based off of Joss Crowcroft's [work](http://josscrowcroft.com/projects/motioncaptcha-jquery-plugin/).*

* [Harmony Ribbon Brush](http://mrdoob.com/projects/harmony/)
* [$1 Unistroke Recognizer (Jacob O. Wobbrock, Ph.D., Andrew D. Wilson, Ph.D., & Yang Li, Ph.D.)](http://depts.washington.edu/aimgroup/proj/dollar/)
* [Bootstrap](http://twitter.github.com/bootstrap/) for the Example/homepage
