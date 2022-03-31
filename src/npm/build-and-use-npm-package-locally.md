# Building and Using NPM Packages Locally

> Links:
> 
> - [Build and use npm package locally](https://stackoverflow.com/questions/55560791/build-and-use-npm-package-locally)

Sometimes it is valuable to alter a package locally and use those changes as a dependency of another project. Once you have amde appropriate changes on your machine.

1. Build the project. Conventially with a *"script"* field in *package.json*, use `npm run build`

2. Go to the parent directory of *dist/* (or wherever the compiled output is)

3. Issue `npm pack`. This will create a *.tgz* compressed file with your custom package.

4. Copy the *.tgz* file into the root of the project you wish to use it in.

5. In *package.json* replace the version number with `"<package_name>": "file:<packed-file>.tgz"`.

6. Issue `npm install` with the new *package.json*

The custom package will now be in your *node_modules/*.




