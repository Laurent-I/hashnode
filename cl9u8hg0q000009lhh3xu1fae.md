---
title: "Migrating Create React App to Vite"
seoTitle: "Migrating a create react app to vite"
seoDescription: "Ever wanted to shift your create react app to vite; well then here is how to do it in very simple and easy ways"
datePublished: Sat Oct 29 2022 18:05:23 GMT+0000 (Coordinated Universal Time)
cuid: cl9u8hg0q000009lhh3xu1fae
slug: migrating-create-react-app-to-vite
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1667063457225/2DnFAoevH.webp
tags: reactjs, intermediate, vite

---

# Moving your Create React App To Vite

If you have ever used Vite or Create React App we know the difference in time it takes for the create-react-app and the vite server.
Many of us (Me included) hate when it takes time to bundle our files and it is really annoying.
So today I am going to show you how to migrate to vite even if you used create-react-app to initialize your project so that we can together with the new and modern way which is **Vite**.


1. You need to delete your node_modules because we will change the package.json file for vite. *(this is optional to do)*


2. Add the following to your package.json file. *(Note that the package versions may change so be sure to use the lastest version)*

```
"devDependencies": {
    "@vitejs/plugin-react": "^2.2.0",
    "vite": "^3.2.1",
    "vite-plugin-html": "^3.2.0"
  }
```
and remove the following from the dependencies object:


```
"dependencies": {
      "react-scripts": 5.0.1,
}
``` 
Then run npm install or yarn add.

Move public/index.html to index.html (project root folder). This is necessary. Otherwise, Vite will not work.

Then we need to modify the index.html file and remove the %PUBLIC_URL% so they look like this:


```
    <link rel="icon" href="/favicon.ico" />
    <link rel="apple-touch-icon" href="/logo192.png" />
    <link rel="manifest" href="/manifest.json" />

``` 
Then add a script entry point in the index.html file

```
    <script type="module" src="/src/index.jsx"></script>
``` 

For typescript users then use your typescript entry point (i.e. /src/index.tsx)
Next step is to create a* vite.config.js or vite.config.ts* file at the root of your project. The file should look like this:

```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";

export default defineConfig({
  plugins: [react()],
});

``` 
Go to your src folder, create a new file vite-env.d.ts and add this line to the file: /// <referencetypes="vite/client" />* (You have to add /// also)*


```
/// <referencetypes="vite/client" />
``` 

If your project isn't that big then it is likely that this are the only steps you will need to make.

## For Big Projects
### Working on the enviroment variables 

In create-react-app most .env files are almost similar with the prefix REACT_APP

```
REACT_APP_TITLE=How To React
REACT_APP_DESCRIPTION=Using .env file in React js
``` 
For vite all environment variables start with  VITE_ by default so we need to change all the REACT_APP_   to VITE_


```
VITE_TITLE=How To React
VITE_DESCRIPTION=Using .env file in React js
``` 
If you have alot of variables that could be hassle for you to change them unless you are persistent. So instead you can install a package called vite-plugin-env-compatible. Run the command in the terminal npm i vite-plugin-env-compatible or yarn add vite-plugin-env-compatible. But also you have to add the following in your * vite.config.js or vite.config.ts* file.


```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import envCompatible from "vite-plugin-env-compatible";

export default defineConfig({
  envPrefix: 'REACT_APP_',


  plugins: [
      react(),
      envCompatible(),
],
});

``` 
The envPrefix tells vite what should be the starting of every env variable. Thus you don’t need to change any of the env variable name. Then we have to change everywhere where you used *process.env* to *import.meta.env*.
This is easy to do since you can search in the editor where you wrote it and simply replace it.

**PS:** If you are using the .js extension on your files it is required to change them to .jsx

# Conclusion
This is how you can easily migrate from create-react-app to vite in simple steps and please feel free to leave a comment on anything that is not correct. So I finish by encouraging you to join me on the sunny side with vite           . Happy coding 💻😁

 








