# Code Snippets - Customizing the "Escapade" WP theme

Hey there! So, I've got this awesome blog called [Code Snippets](https://codesnippets.freewebtools.net), which is my little corner of the internet where I share helpful coding tips and tricks with the world. I use the [Escapade](https://github.com/godaddy-wordpress/primer-child-escapade) WordPress theme as a starting point, but I jazz it up with my own custom JavaScript, jQuery, and CSS code to really make it my own and give it some personality.


## Required WP Plugin

In order to add custom JavaScript and jQuery code to modify the [Escapade](https://github.com/godaddy-wordpress/primer-child-escapade) WordPress theme, I use the [CM Header & Footer Script Loader](https://wordpress.org/plugins/cm-header-footer-script-loader/) WP plug-in. It's super easy to use and lets you add your own code to the header or footer of your WordPress site. Plus, it's a great way to keep your code separate from your theme files, so you can update your theme without losing any of your customizations.


## Instructions/Installation

- Install the  [CM Header & Footer Script Loader](https://wordpress.org/plugins/cm-header-footer-script-loader/) WP plug-in.
- Go to the General Settings page of the CM Header & Footer Script Loader WP plug-in.
- Add your first script. Select **CSS** as the **Script type**, select **Header Script** as the **Script Location**, and make sure the **Autoload Option** has the **Load by default on All Posts and Pages** option selected. Add the following CSS code to the textarea:

```
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet">
```

- Add a new script. Select **JS** as the **Script type**, select **Footer Script** as the **Script Location**, and make sure the **Autoload Option** has the **Load by default on All Posts and Pages** option selected. Add the following JS code to the textarea:

```
<!-- https://jsfiddle.net/tovic/AbpRD/  -->
<script>
	(function() {
    	var pre = document.getElementsByTagName('pre'), pl = pre.length;
    	for (var i = 0; i < pl; i++) {
        	pre[i].innerHTML = '<span class="line-number"></span>' + pre[i].innerHTML + '<span class="cl"></span>';
        	var num = pre[i].innerHTML.split(/\n/).length;
        	for (var j = 0; j < num; j++) {
            	var line_num = pre[i].getElementsByTagName('span')[0];
            	line_num.innerHTML += '<span>' + (j + 1) + '</span>';
        	}
   		}
	})();

	document.getElementsByName("s")[0].placeholder="C:\\>";
</script>


<script>
    var i;

    for (i = 0; i < document.getElementsByClassName("site-info-text").length; i++) {

        var yourHTML = '<br><br>Copyright © 2023 Code Snippets — Free Web Tools by <a href="https://astralmemories.com" target="_blank" class="footer-copyright-link">Astral Memories</a>';

        document.getElementsByClassName("site-info-text")[i].innerHTML = yourHTML;

    }
</script>


<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=VT323&display=swap" rel="stylesheet"> 

<script src="https://code.jquery.com/jquery-3.6.4.min.js" integrity="sha256-oP6HI9z1XaZNBrJURtCoUT5SUnxFr8s3BzRl+cbzUq8="crossorigin="anonymous"></script>

<script>
	$(".side-masthead").prepend("<canvas id='canvas'></canvas>");
</script>

<script>
    var c = document.getElementById("canvas");
	var ctx = c.getContext("2d");

    // Assign the canvas size
    c.height = $("#site-navigation")[0].offsetHeight + $(".site-title-wrapper")[0].offsetWidth + 40;
    c.width = $("#site-navigation")[0].offsetWidth;

    // Characters
    var matrix = "€†‡Š‹ŒŽ˜šœžŸ¢£¤¥¦§«¬±°µ¶ÂÃÆÊÐØÛÝÞßæèçêð÷øÿþĄĎĐđĒĔĘĚĜĢĦħĬĮįĳĴĶĹĿłŁŊŋŒŞƁƂƀƇƅƎƏƐƍƔƓƕƙƚƛƞƝƟƠƢƤƣƥƩƫƮƴƳƱƲƻƺƾƿǂǮǶȚǼǽȢȣȠȡȴȶɎɏɇɆɄɃɀʎʢʡʞʠɷɸʄʆʈʭʉʋɣȾΘΏΔΞΓΣΦΩΨϓϔϕϖψφϪϬωϭϠϡϢϣϗЂϼЉЋЎЏ";
    // Converting the string into an array of single characters
    matrix = matrix.split("");

    var font_size = 10;
    var columns = c.width/font_size; //number of columns for the rain
        
    // An array of drops - one per column
    var drops = [];
    
    // x below is the x coordinate
    // 1 = y co-ordinate of the drop (same for every drop initially)
    for(var x = 0; x < columns; x++)
    {
    	drops[x] = 1;
    }
        

    // Drawing the characters
    function draw()
    {
        // Black BG for the canvas
        // Translucent BG to show trail
        ctx.fillStyle = "rgba(0, 0, 0, 0.04)";
        ctx.fillRect(0, 0, c.width, c.height);

        ctx.fillStyle = "yellowgreen"; //green text
        ctx.font = font_size + "px arial";
        // Looping over drops
        for (var i = 0; i < drops.length; i++)
        {
            // A random character to print
            var text = matrix[Math.floor(Math.random()*matrix.length)];
                
            // x = i*font_size, y = value of drops[i]*font_size
            ctx.fillText(text, i*font_size, drops[i]*font_size);

            // Sending the drop back to the top randomly after it has crossed the screen
            // Adding a randomness to the reset to make the drops scattered on the Y axis
            if(drops[i]*font_size > c.height && Math.random() > 0.975)
            {
            	drops[i] = 0;
            }

            // Incrementing Y coordinate
            drops[i]++;
        }
    }

    setInterval(draw, 35);

	$(window).on('resize', function(){
    	// Assign the canvas size
    	c.height = $("#site-navigation")[0].offsetHeight + $(".site-title-wrapper")[0].offsetWidth + 40;
    	c.width = $("#site-navigation")[0].offsetWidth;
    	
    	columns = c.width/font_size; //number of columns for the rain
        
    	// An array of drops - one per column
    	drops = [];
    	
    	// x below is the x coordinate
    	// 1 = y co-ordinate of the drop (same for every drop initially)
    	for(var x = 0; x < columns; x++)
    	{
    		drops[x] = 1;
    	}
	});
</script>
```

- Click the **Save Changes** button to save the CSS and JavaScript code.
- Go to the **Customize** admin page of your **Escapade** theme (**Appearance** -> **Customize**), and open the **Additional CSS** section. Add the following CSS code:

```
/* Global Settings */
div#primary {
	width: 100%;
}
code {
	background-color: black;
	color: green;
}
pre {
	background-color: black;
	color: #1aff00;
}
	textarea#comment {
    background: #191919 !important;
}
	input {
    background: #191919 !important;
}

.site-description {
    color: #55b74e;
}
.side-masthead {
  overflow: scroll !important;
  height: 100% !important;
}

h2.entry-title {
  font-size: 2em !important;
	font-weight: 500 !important;
}

h2 {
    font-size: 2rem !important;
	  font-weight: 500 !important;
}

.entry-header-column h1 {
  font-size: 3em !important;
	font-weight: 500 !important;
}

h1 {
    font-size: 3rem !important;
	  font-weight: 500 !important;
}

.site-main article {
  padding: 0.5rem 3.5rem !important;
}

.wp-block-search__inside-wrapper {
  flex-flow: row;
  align-items: baseline;
}

.wp-block-search__input {
  color: #1aff00 !important;
}

code {
  color: #1aff00 !important;
  border-color: rgba(229, 229, 229, 0) !important;
}

a, a:visited {
  
  text-shadow: 1px 1px 1px #00ff00, 0 0 1vmin #00ff00, 0 0 1px #00ff00;
  text-decoration: none;
}

a:hover, hr {
  color: #00ff00;
}

#page {
	font-family: 'Share Tech Mono', monospace;
}

.side-masthead {
	font-family: 'VT323', monospace !important;
  background: rgba(0, 0, 0, .3);
}

h1, h2, h3, h4, h5, h6, label, legend, table th, dl dt, .entry-title, .widget-title {
  font-family: 'VT323', monospace !important;
}

blockquote, .entry-meta, .entry-footer, .comment-list li .comment-meta .says, .comment-list li .comment-metadata, .comment-reply-link, #respond .logged-in-as {
  font-family: 'VT323', monospace !important;
	font-size: 18px;
}

h1, h2, h3, h4, h5, h6 {
  line-height: 1;
}

ul, ol, dl {
  line-height: 1;
}

.footer-menu ul li a:hover, .footer-menu ul li a:visited:hover {
  color: #00ff00;
}

.nav-previous a:hover {
	color: #00ff00;
}

.nav-next a:hover {
	color: #00ff00;
}

/* Mouse Cursors */
body {
  cursor: url("/cursors/default.cur"), default;
}

a:hover {
  cursor: url("/cursors/pointer.cur"), pointer;
}

input:hover {
  cursor: url("/cursors/text.cur"), text;
}

button:hover {
  cursor: url("/cursors/pointer.cur"), pointer;
}

#menu-toggle:hover {
  cursor: url("/cursors/pointer.cur"), pointer;
}

/* Site Header */
.site-header {
  padding: 70px 0 !important;
}

@media (max-width:881px) {
	.site-header {
  padding: unset !important;
  }
}

/* Site Title / Site Logo */
.site-title {
  font-family: 'VT323', monospace !important;
	text-align: center;
}

#menu-primary-menu {
	font-family: 'VT323', monospace !important;
}

body, p, ol li, ul li, dl dd, .fl-callout-text {
  font-family: 'VT323', monospace !important;
}

.site-title-wrapper {
  background-color: black;
  background-image: radial-gradient(rgba(0, 150, 0, 0.75), black 120%);
  overflow: hidden;
  color: white;
  text-shadow: 0 0 5px #C8C8C8;
	border: solid yellowgreen;
	box-shadow: 1px 1px 1px #00ff00, 0 0 1vmin #00ff00, 0 0 1px #00ff00;
	border-radius: 10px;
}

.site-title-wrapper::after {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: repeating-linear-gradient(0deg, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2) 1px, transparent 1px, transparent 2px);
  pointer-events: none;
}

.site-title-wrapper {
	animation: flicker 0.5s infinite, glitch-skew 1.033s infinite;
}

#menu-toggle {
	text-shadow: 0 0 5px #C8C8C8;
	animation: flicker 0.5s infinite;
}

.site-description {
	color: yellowgreen;
}

.site-description::after {
	content: "\2590";
	animation: intermitent 1.2s infinite;
}

.flicker {
  pointer-events: none;
  position: fixed;
  width: auto;
  min-width: 100%;
  height:100%;
  z-index:15;
  background: rgba(9, 8, 8, 0.1);
  animation: flicker 0.3301s infinite;
}

@keyframes flicker {
	0% {
		opacity: 0.9;
	}
	5% {
		opacity: 0.95;
	}
	10% {
		opacity: 0.9;
	}
	15% {
		opacity: 0.9;
	}
	20% {
		opacity: 0.9408;
	}
	25% {
		opacity: 0.9;
	}
	30% {
		opacity: 0.9;
	}
	35% {
		opacity: 0.85;
	}
	40% {
		opacity: 1;
	}
	45% {
		opacity: 1;
	}
	50% {
		opacity: 0.99436;
	}
	55% {
		opacity: 0.9574;
	}
	60% {
		opacity: 0.9;
	}
	65% {
		opacity: 0.98;
	}
	70% {
		opacity: 1;
	}
	75% {
		opacity: 1;
	}
	80% {
		opacity: 1;
	}
	85% {
		opacity: 1;
	}
	90% {
		opacity: 1;
	}
	95% {
		opacity: 0.95;
	}
	100% {
		opacity: 1;
	}
}

@keyframes glitch-skew {
    0% {
        transform: skew(0deg, 0deg);
    }
    48% {
        transform: skew(0deg, 0deg);
        filter: blur(0);
    }
    50% {
        transform: skew(-5deg, 0deg);
        filter: blur(4px);
    }
    52% {
        transform: skew(5deg, 0deg);
    }
    54% {
        transform: skew(0deg, 0deg);
        filter: blur(0);
    }
    100% {
        transform: skew(0deg, 0deg);
    }
}

.site-description {
  margin: 0 0 8px 0px;
}

@media (max-width:881px) {
	.site-description {
    display: none;
    float: none;
  }
	.site-title {
    margin: 0px;
  }
}

/* Main Navigation */
.main-navigation ul li a, .main-navigation ul li a:visited, button, a.button, a.fl-button, input[type="button"], input[type="reset"], input[type="submit"] {
  font-family: 'VT323', monospace !important;
}

#menu-primary-menu .menu-item {
  background-color: rgba(0, 0, 0, 0.3);
  background-image: radial-gradient(rgba(0, 150, 0, 0.75), black 120%);
  overflow: hidden;
  color: white;
  text-shadow: 0 0 5px #C8C8C8;
	box-shadow: 1px 1px 1px #00ff00, 0 0 1vmin #00ff00, 0 0 1px #00ff00;
}

#menu-primary-menu .menu-item::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: repeating-linear-gradient(0deg, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2) 1px, transparent 1px, transparent 2px);
  pointer-events: none;
}

#menu-primary-menu .menu-item:hover {
  background-color: rgba(85, 183, 78, 0.8);
  border-color: rgba(85, 183, 78, 0.8);
}

#menu-primary-menu .current-menu-item {
  background-color: rgba(85, 183, 78, 0.8);
  border-color: rgba(85, 183, 78, 0.8);
	background-image: none;
}

.menu-item:hover a::after {
  /* https://www.htmlsymbols.xyz/unicode/U+2590 */
	content: "\2590";
	animation: intermitent 1.2s infinite;
}

@keyframes intermitent {
	0% {
		opacity: 0;
	}
	10% {
		opacity: 0;
	}
	20% {
		opacity: 0;
	}
	30% {
		opacity: 0;
	}
	40% {
		opacity: 0;
	}
	50% {
		opacity: 1;
	}
	60% {
		opacity: 1;
	}
	70% {
		opacity: 1;
	}
	80% {
		opacity: 1;
	}
	90% {
		opacity: 1;
	}
	100% {
		opacity: 1;
	}
}

/* Site Borders */
:root {
  --main-border-color: yellowgreen;
	/* --main-border-color: #5330E1; */
	--main-boder-style: double;
}

body {
  border-right: var(--main-boder-style) var(--main-border-color) 4px;
}

@media (max-width:881px) {
  body {
    border-left: var(--main-boder-style) var(--main-border-color) 4px;
  }
}

#masthead {
	border-top: var(--main-boder-style) var(--main-border-color) 4px;
}

.content-area {
  border-top: var(--main-boder-style) var(--main-border-color) 4px;
}

.site-info-wrapper {
	border-bottom: var(--main-boder-style) var(--main-border-color) 4px;
}

.side-masthead {
  border-right: var(--main-boder-style) var(--main-border-color) 4px;
}

@media (max-width:881px) {
	.side-masthead {
    border-right: none;
  }
}

/* Continue Reading Button */
.entry-summary .button {
  background-color: black;
  background-image: radial-gradient(rgba(0, 150, 0, 0.75), black 120%);
  overflow: hidden;
  color: white;
  text-shadow: 0 0 5px #C8C8C8;
	border: solid rgba(85, 183, 78, 0.8);
	box-shadow: 1px 1px 1px #00ff00, 0 0 1vmin #00ff00, 0 0 1px #00ff00;
	border-radius: 10px;
}

.entry-summary .button:hover {
	border: solid #00ff00;
	background-color: rgba(85, 183, 78, 0.8);
	background-image: none;
}

/* Donate Button Section */
.footer-widget .button {
  background-color: black;
  background-image: radial-gradient(rgba(0, 150, 0, 0.75), black 120%);
  overflow: hidden;
  color: white;
  text-shadow: 0 0 5px #C8C8C8;
	border: solid rgba(85, 183, 78, 0.8);
	box-shadow: 1px 1px 1px #00ff00, 0 0 1vmin #00ff00, 0 0 1px #00ff00;
	border-radius: 10px;
}

.footer-widget .button:hover {
	border: solid #00ff00;
	background-color: rgba(85, 183, 78, 0.8);
	background-image: none;
}

.footer-widget-area {
  padding: 1rem 4.7rem 0rem 4.7rem;
}

/* Search Button */
.wp-block-search__button {
  background-color: black;
  background-image: radial-gradient(rgba(0, 150, 0, 0.75), black 120%);
  overflow: hidden;
  color: white;
  text-shadow: 0 0 5px #C8C8C8;
	border: solid rgba(85, 183, 78, 0.8);
	box-shadow: 1px 1px 1px #00ff00, 0 0 1vmin #00ff00, 0 0 1px #00ff00;
	border-radius: 10px;
	white-space: nowrap;
	padding: 0px 25px 0px 25px;
  width: 35%;
}

.wp-block-search__button:hover {
	border: solid #00ff00;
	background-color: rgba(85, 183, 78, 0.8);
	background-image: none;
}

.wp-block-search__input {
	font-family: 'VT323', monospace !important;
}

/* Old Terminal Effect */
body::after {
  content: "";
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: repeating-linear-gradient(0deg, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.2) 1px, transparent 1px, transparent 2px);
  pointer-events: none;
}

#page {
	background-image: radial-gradient(rgba(16, 36, 0, 0.75), black 100%);
}

/* Code and Pre line numbers */
/* https://jsfiddle.net/tovic/AbpRD/ */
pre code,
pre .line-number {
  font:normal normal 12px/14px "Courier New",Courier,Monospace;
  color:darkgreen;
  display:block;
}

pre .line-number {
  float:left;
  margin:0 1em 0 -1em;
  border-right:1px solid;
  text-align:right;
	user-select: none;
}

pre .line-number span {
  display:block;
  padding:0 .5em 0 1em;
}

pre .cl {
  display:block;
  clear:both;
}

/* Code Pre overflow-wrap */
.wp-block-code code {
	white-space: pre;
}

#canvas {
  display: block;
  position: absolute;
  top: 0px;
  left: 0px;
}
```
- To add the custom cursors to your WordPress site, download/clone this repository and copy the **cursors** folder to the root directory of your WordPress site.

## Thank you!
If you find this useful and would like to show your appreciation, consider buying me a cup of coffee. Your support is greatly appreciated and helps me continue creating valuable content. Thank you!

[Donate](https://www.paypal.com/donate/?hosted_button_id=TTU5PDRRJGKM2)

[![](https://codesnippets.freewebtools.net/wp-content/uploads/2023/04/QR-Code.png)](https://codesnippets.freewebtools.net/wp-content/uploads/2023/04/QR-Code.png)
