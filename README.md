# How To Create npm Package & Publish
Steps to create npm package and publish to npmjs.com

### Step1: Create a folder
### Step2: Within the folder, run [npm init] or [npm init -y] through CMD. It will create the [package.json] file.
### Step3: Edit the package.json file as per your requirements
```javascript
{
  "name": "@arindam/console-color",
  "version": "1.0.0",
  "description": "A library to print console log in different colors. Like: danger, success, info, highlight",
  "main": "./dist/index.js",
  "module": "./dist/index.mjs",
  "types": "./dist/index.d.ts",
  "scripts": {
    "build": "tsup",
    "prepare": "npm run build"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/dev-arindam-roy/npm-console-color"
  },
  "keywords": ["devarindam", "console color", "console color log", "console log"],
  "author": "Arindam Roy <arindam.roy.developer@gmail.com> (https://github.com/dev-arindam-roy)",
  "license": "MIT",
  "bugs": {
    "url": "https://github.com/dev-arindam-roy/npm-console-color/issues"
  },
  "homepage": "https://github.com/dev-arindam-roy/npm-console-color#readme",
  "devDependencies": {
    "tsup": "^8.0.2",
    "typescript": "^5.3.3"
  },
  "dependencies": {
    
  }
}
```
### Step4: Install typescript globaly [npm install -g typescript]
### Step5: Install package development dependencies [npm install -D typescript tsup]
### Step6: Create a file name "tsconfig.json" and write/edit below code as your requirements
```javascript
{
    "compilerOptions": {
        "strict": true,
        "noImplicitAny": true,
        "esModuleInterop": true,
        "strictNullChecks": true,
        "target": "ES2017",
        "moduleResolution": "Node",
        "module": "CommonJS",
        "declaration": true,
        "isolatedModules": true,
        "noEmit": true,
        "outDir": "dist"
    },
    "include": ["src"],
    "exclude": ["node_modules", "**/__test__/*"]
}
```
### Step7: Create a file name "tsup.config.ts" and write/edit below code as your requirements
```javascript
import { defineConfig } from 'tsup';

export default defineConfig ({
    format: ['cjs', 'esm'],
    entry: ['./src/index.ts'],
    dts: true,
    shims: true,
    skipNodeModulesBundle: true,
    clean: true
});
```
### Step8: Write your package business logic or code in the 'src' folder, like below:
```javascript
export class ColorLog {

    /** Use for success console log */
    static success(msg:string) {
        console.log(`%c ${msg}`, 'color: green');
    }

    /** Use for error console log */
    static danger(msg:string) {
        console.log(`%c ${msg}`, 'color: red');
    }

    /** Use for information/statement console log */
    static info(msg:string) {
        console.log(`%c ${msg}`, 'color: blue');
    }

    /** Use for highlight something console log */
    static highlight(msg:string) {
        console.log(`%c ${msg}`, 'color: black; background: yellow');
    }
}
```
### Step9: To build the package run [npm run build]
### Step10: The build version will be created in the 'dist' folder
### Step11: Create 2 more files - '.gitignore' & '.npmignore'
### Step12: In the '.gitignore'
```javascript
/dist
/node_modules

.env
.DS_Store

package-lock.json
```
### Step13: In the '.npmignore'
```javascript
/src
/node_modules

.env
.DS_Store

doc.txt

tsconfig.json
tsup.config.ts
package-lock.json
```
### Step14: First push in git repo
### Step15: Then publish it npmjs.com by below commands
```javascript
npm login 
npm publish
```

### Step16: For testing [npm link]
### Step17: In another test folder [npm link _your_package_name_]

### NOTE:
```javascript
For package development, 3 files is important
1) package.json // use for package information.
2) tsconfig.json // use for output directory and other build settings
3) tsup.config.ts // use tsup for build the package ["build": "tsup"]
```

