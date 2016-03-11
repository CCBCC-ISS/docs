# Web Application Project Structure

## Proposed Project Organization
Applications and projects should be broken down in a fractal fashion that favors grouping files by feature & functionality rather than file type.

As an example:
```

<Project Name>
|
|__<Backend folder> (if it's included or required)
|
|__app/
	|
	|shared/
	|	|
	|	|_(potentially globally used files could be contained here) 
	|
	|home/ (home screen/landing page)
	|	|
	|	|__index.html
	|	|__app.js
	|	|__style.css
	|
	|admin/ (admin portal)
		|
		|__admin.html
		|__admin.js
		|__permissions.js (control who can access the admin portal)
		|__admin.css	
...

```

In the above example, all of the code related to the home screen of a hypothetical web application is contained in one location. Likewise for an admin portal. There are placeholders for folders for back end code or globally shared files in the project, but most of the files are under the folders that represent their functionality. 

The shared folder could contain code such as a base prototypes/classese of JavaScript objects.