# Understanding *NPM* Packages

## Where Does *NPM* Install Packages?

NPM packages can be either global or local to a project. To install a packge globally use `npm i -g <package>`; to see the global packages use `npm list -g`. Usually it is advisable to not install packages globally and install install them with `npm i <package>`. In this case they will be installed into the *node_modules/* folder in the package where they're used. Use `npm list` to see the local packages in your current project.

>  Note: Having the same package installed both globally and locally can cause dependency conflicts.

To make dependency management easier, when you install a new package with `npm i <package>` it will add it to the "dependencies" field in *package.json*. This allows other developers to run `npm i` and all of the stated dependencies will be installed without having to specify them individually.

## Scoped Packages

In *NPM* there is a concept called *scoped packages*, which allows packages to be namespaced. Users and organizations on *NPM* are given a scope to which only they can add packages to. Scoped packages are installed in the *node_modules/@scope_specifier/* directory. 
