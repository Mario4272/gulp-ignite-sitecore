# gulp-ignite-sitecore

[![Build Status](https://travis-ci.org/jscarmona/gulp-ignite-sitecore.svg?branch=master)](https://travis-ci.org/jscarmona/gulp-ignite-sitecore)
[![npm](https://img.shields.io/npm/dt/gulp-ignite-sitecore.svg?maxAge=2592000)]()
[![GitHub tag](https://img.shields.io/github/release/jscarmona/gulp-ignite-sitecore.svg?maxAge=2592000)]()

Inspired by [Sitecore Habitat](https://github.com/Sitecore/Habitat)

## install

**NPM**

```sh
npm i -D gulp-ignite gulp-ignite-sitecore
```

## setup

```js
'use strict';

import ignite from 'gulp-ignite';
import * as sitecore from 'gulp-ignite-sitecore';

const tasks = Object.keys(sitecore).map(k => sitecore[k])];
const options = {
  'sitecore:copy-sitecore-libraries': {
    src: 'C:\\Websites\\Sitecore\\Website',
  },
  'sitecore:nuget-restore': {
    solutionName: 'sitecore',
  },
  'sitecore:publish-projects': {
    configuration: 'Debug',
    dest: 'C:\\Websites\\Sitecore\\Website',
  },
  'sitecore:publish-tds': {
    configuration: 'Debug',
    options: {
      properties: {
        SitecoreDeployFolder : 'C:\\Websites\\Sitecore\\Website',
        SitecoreWebUrl : 'http://sitecore',
      },
    },
  },
  'sitecore:deploy': {
    dest: 'C:\\Websites\\Sitecore\\Website',
  },
};

ignite.start(tasks, options);

```

## usage

* [Copy Sitecore Libraries](#copySitecoreLibraries)
* [Restore NuGet Packages](#nugetRestore)
* [Publish Projects](#publishProjects)
* [Publish TDS](#publishTDS)
* [Deploy](#deploy)
* Transforms (Coming Soon)
* Package Website (Coming Soon)
* Sync Unicorn (Coming Soon)


### <a name="copySitecoreLibraries"></a>copy sitecore libraries

Copy the sitecore libaries from the website to `./lib/Sitecore`.

```
gulp sitecore:copy-sitecore-libraries
```

##### arguments
- `--src, -s` - Source directory for sitecore libraries.
- `--dest, -d` - Destination directory.

##### options
- `src` - Source directory for sitecore libraries. (**Required**)
- `dest` - Destination directory. (**Default:** `./lib/Sitecore`)
- `deps` - Any gulp tasks that task would be dependent of. (**Default:** `[]`)

---

### <a name="nugetRestore"></a>restore nuget packages

Restore all nuget packages for solution.

```
gulp sitecore:nuget-restore
```

##### arguments
- `--solution, -s` - Solution file path.

##### options
- `solution` - Solution file path. (**Required**)
- `deps` - Any gulp tasks that task would be dependent of. (**Default:** `[]`)

---

### <a name="publishProjects"></a>publish projects

Build and publish all projects.

```
gulp sitecore:publish-projects
```

##### arguments
- `--build, -b` - Build configuration.
- `--src, -s` - Publish all `.csproj` files located within directory.
- `--dest, -d` - Destination directory for deployment.
- `--clean, -c` - Perform a clean before a build.

##### options
- `configuration` - Build configuration. (**Default:** `Debug`)
- `dest` - Destination directory for deployment. (**Required**)
- `src` - Publish all `.csproj` files located within directory. (**Default:** `./src`)
- `options` - MSbuild options. (**Default:** `{}`)
- `deps` - Any gulp tasks that task would be dependent of. (**Default:** `[]`)

---

### <a name="publishTDS"></a>publish tds

Publish all TDS projects.

```
gulp sitecore:publish-tds
```

##### arguments
- `--build, -b` - Build configuration.
- `--src, -s` - Publish all `.scproj `files located within directory.
- `--dest, -d` - Destination directory for deployment.
- `--url, -u` - Destination sitecore url for deployment.

##### options
- `options` - MSbuild options. (**Required**)
  - `properties` (Overwrites for values set in VisualStudio)
    - `SitecoreWebUrl` - Destination sitecore url for deployment
    - `SitecoreDeployFolder` - Destination directory for deployment
    - `OutputPath` - Path to output item files (**Default** `.\\bin\\Debug`)
- `configuration` - Build configuration. (**Default:** `Debug`)
- `src` - Publish all `.scproj `files located within directory. (**Default:** `./src`)
- `deps` - Any gulp tasks that task would be dependent of. (**Default:** `[]`)

---

### <a name="deploy"></a>deploy

Deploy files to Sitecore website

```
gulp sitecore:deploy
```

##### arguments
- `--watch, -w` - Watch files for changes and auto deploys.

##### options
- `dest` - Destination directory for deployment. (**Required**)
- `src` - Files to deploy. (**Default:** `[]`)
- `watchFiles` - Files to watch (**Default:** `[]`)


## license

The MIT License (MIT)

Copyright (c) 2016 Javier Carmona

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
