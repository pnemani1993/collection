# Node Package Manager #
What is a package in javascript? 
: A package is a file or directory that is described by a package.json file. A package must contain a package.json file in order to be published to the npm registry.

What is a module? 
: A module is any file or directory in the node_modules directory that can be loaded by the Node.js require() function.
To be loaded by the Node.js require() function, a module must be one of the following:
- A folder with a package.json file containing a "main" field.
- A JavaScript file.

## To install the latest version of npm ##

```bash
npm install npm@latest -g
```
For creating an empty package.json file for unscoped module. 
For scoped module use `npm init --scope=@scope-name`
```bash
npm init
```
For creating a package.json file based on the current directory containing the following information: 
```bash
npm init --yes
```
```json package.json
{
  "name": "my_package",
  "description": "",
  "version": "1.0.0",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "https://github.com/monatheoctocat/my_package.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/monatheoctocat/my_package/issues"
  },
  "homepage": "https://github.com/monatheoctocat/my_package"
}
```

Node.js modules are a type of package that can be published to npm. To be able to do that: 
1. Create a package.json file. 
2. Create the file that will be loaded when the module is required by another application. 
3. Test your module. 

> [What should the package.json file contain?](https://docs.npmjs.com/cli/v10/configuring-npm/package-json) 

Installing modules locally and globally: 
- Local install (default): puts stuff in ./node_modules of the current package root.
- Global install (with -g): puts stuff in /usr/local or wherever node is installed. 

## Keeping files out of your Package ##

Use a `.npmignore` file to keep stuff out of your package. If there's no `.npmignore` file, but there is a `.gitignore` file, then npm will ignore the stuff matched by the .gitignore file. If you want to include something that is excluded by your `.gitignore` file, you can create an empty .npmignore file to override it. Like git, npm looks for `.npmignore` and `.gitignore` files in all subdirectories of your package, not only the root directory.

## Pre & Post Scripts ##

To create "pre" or "post" scripts for any scripts defined in the "scripts" section of the package.json, simply create another script with a matching name and add "pre" or "post" to the beginning of them.
```json
{
  "scripts": {
    "precompress": "{{ executes BEFORE the `compress` script }}",
    "compress": "{{ run command to compress files }}",
    "postcompress": "{{ executes AFTER `compress` script }}"
  }
}
```
In this example npm run compress would execute these scripts as described.