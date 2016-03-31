# FSOP eTool Performance and Suggested Improvments

CSS Loading
---
* [Jake Archibald](https://jakearchibald.com/2016/link-in-body/) has a great post about using `<link>` in `<body>` to achieve backward-compatible progressive rendering.

Website Perfomance
---
*as of March 4, 2016*

### Load Times
Load time was measured three times against the Dev site to get an average over VPN. 
The cache was emptied and a hard reload was performed.
All tests were performed in Chrome Canary 51.0.2665.0 (64-bit).
<table>
	<thead>
		<tr>
			<th></th>
			<th>Finish</th>
			<th>DOMContentLoaded</th>
			<th>Load</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Run 1</td>
			<td>2.57s</td>
			<td>1.92s</td>
			<td>1.94s</td>	
		</tr>
		<tr>
			<td>Run 2</td>
			<td>2.19s</td>
			<td>1.61s</td>
			<td>1.64s</td>	
		</tr>
		<tr>
			<td>Run 3</td>
			<td>2.15s</td>
			<td>1.73s</td>
			<td>2.17s</td>	
		</tr>
	</tbody>
	<tfoot>
		<tr>
			<td><b>Average</b></td>
			<td>2.30s</td>
			<td>1.75s</td>
			<td>1.92s</td>
		</tr>
	</tfoot>
</table>

---
*as of March 31, 2016*

### Load Times
Load time was measured three times against the Dev site to get an average over VPN. 
The cache was emptied before each test.

#### Safar Developer Preview Version 9.1.1 (11601.6.10, 11602.1.25)
* 52 files transferred
* 2.38 MB transferred

<table>
    <thead>
	<tr>
	    <th>DOMContentLoaded</th>
	    <th>Load</th>
	</tr>
    </thead>
    <tbody>
	<tr>
	    <td>1.59 s</td>
	    <td>1.98 s</td>
	</tr>
	<tr>
	    <td>1.48 s</td>
	    <td>1.52 s</td>
	</tr>
	<tr>
	    <td>1.73 s</td>
	    <td>2.43 s</td>
	</tr>
	<tr>
	    <td>1.24 s</td>
	    <td>1.29 s</td>
	</tr> 
	<tr>
	    <td>1.55 s</td>
	    <td>1.60 s</td>
	</tr> 
	<tr>
	    <td>1.85 s</td>
	    <td>1.88 s</td>
	</tr> 
	<tr>
	    <td>2.32 s</td>
	    <td>2.37 s</td>
	</tr>
	<tr>
	    <td>2.33 s</td>
	    <td>2.72 s</td>
	</tr>
    </tbody>
</table>

---
Suggestions
---
Improving load times:
* Minify CSS
	* `components.css`
	* `plugins.css`
	* `layout.css`
	* `dark.css`
	* `custom.css`
	* **Some CSS files have `.min` in their name but are not actually minified** (like `jquery.notific8.min.css`)

* Remove state-dependent CSS files from `index.html` 
	* `ng-tags-input*.css`
	* `*ui-tree*.css`

* Minify/Uglify JS files
	* `app.js`
	* `directives.js` (also break out directives into their own files; some may not be necessary in every state.
	* `metronic.js`
	* `layout.js`

* Either remove the request for the user profile image or fix the server response.


Notes
---

Having so many resources pulled down to the device on initial load will 
