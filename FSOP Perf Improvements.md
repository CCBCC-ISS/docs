# FSOP eTool Performance and Suggested Improvments

CSS Loading
---
* [Jake Archibald](https://jakearchibald.com/2016/link-in-body/) has a great post about using `<link>` in `<body>` to achieve backward-compatible progressive rendering.

Website Perfomance
---
*as of March 4, 2016*

### Load Times
Load time was measured three times against the QA site to get an average over VPN. 
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