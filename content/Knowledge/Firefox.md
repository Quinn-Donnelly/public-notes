Move to firefox and first step is extensions and management
1. [Sideberry](https://github.com/mbnuqw/sidebery)
	1. Tab groups and tab trees together
	2. Also modified my profile to hide the tabs since I will now manage them in the side bar
	    Find your profile folder (hence referred to as ${PROFILE}): go to about:support and look at the line that says "Profile folder".
	    Toggle the relevant about:config flags.
	    - **`toolkit.legacyUserProfileCustomizations.stylesheets`**
		- **`layers.acceleration.force-enabled`**
		- **`gfx.webrender.all`**
		- **`gfx.webrender.enabled`**
		- **`layout.css.backdrop-filter.enabled`**
		- **`svg.context-properties.content.enabled`**
	    Close Firefox.
	    Put this in ${PROFILE}/chrome/userChrome.css (create the file if it doesn't already exist):
		```css
	#TabsToolbar
	{
	    visibility: collapse;
	}
	```
		Start up Firefox again.
		For the second bit, I think if you check the "Title bar" box when you go to "Customize" (Menu -> More Tools -> Customize Toolbar), it'll display your OS's title bar.
1. Setup darkreader the same way it was in chrome 