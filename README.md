# theme-correct-favicon
Switch out your favicon whenever a user changes their browser theme for a better UX.

I have used React for the example because it is most likely a more wholesome example. If any changes are necessary for the script to be compatible to a different framework, then let me know and I can add another example here.

### Use cases
1. Detect users desktop or browser theme
2. Switch your `favicon.ico` files out for another when a user changes their theme to avoid bad UX and your favicon design or image not being visible to a user.
3. Switch out `apple-touch-icon` files, `manifest.json` files or any other icon/asset/stylesheet which will need to change based on the users theme.

### You will need
- A dark mode and light mode compatible icon design. This will usually require swapping out dark colors for light, or visa versa, when designing your icon.
- If you haven't already, convert your icon file (usually a PNG) to a `.ico` for a favicon and to anything else you will need e.g. `apple-touch-icon.png`.

### Core concept
- A dark mode folder and light mode folder will contain the relevant assets.
- Using JavaScipt, an event handler is attached to a browser window event.
- Once that event is fired, the favicon asset file paths are modified on the DOM level.

e.g. User switches browser theme from light to dark mode
`light/favicon.ico` gets changed to `dark/favicon.ico`.

## React example - `react-example/src/index.html`
```
<link rel="apple-touch-icon" sizes="180x180" href="%PUBLIC_URL%/dark/apple-touch-icon.png" />
<link rel="icon" type="image/png" sizes="32x32" href="%PUBLIC_URL%/dark/favicon-32x32.png" />
<link rel="icon" type="image/png" sizes="16x16" href="%PUBLIC_URL%/dark/favicon-16x16.png" />
<link rel="manifest" href="%PUBLIC_URL%/dark/manifest.json" />

<script>
	const onUpdateTheme = (event) => {
		document.querySelectorAll(
			[
				"link[rel='icon']",
				"link[rel='apple-touch-icon']",
				"link[rel='manifest']"
			].join(", ")
		)
		.forEach((element) => {
			element.href = element.href.replace(/\/dark\/|\/light\//g, event.matches ? "/dark/" : "/light/")
		});
	};

	matcher = window.matchMedia("(prefers-color-scheme: dark)");
	matcher.addListener(onUpdateTheme);
	onUpdateTheme(matcher);
</script>
```

#### Steps to run
- Execute `npm install` in `react-example/` directory.
- Execute `npm start` in the `react-example/` directory to run the app.
- Change your desktop theme to see the favicon switch on the browser tab.