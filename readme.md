# taco

a taco themed modular deployment system for unix

![taco.png](taco.png)

[![NPM](https://nodei.co/npm/taco.png)](https://nodei.co/npm/taco/)

### components

- `taco-build` - takes a tarball, runs a build script inside it, and outputs a tarball
- `taco-deploy-mongroup` - deploys tarball using mongroup
- `taco-pack` - creates tarball of an application
- `taco-nginx` - takes a tarball and updates a nginx configuration based on tarball metadata (package.json)

## example

on client:

we recommend setting a `start-production` script in your package.json. taco deploy tools will use `start-production` or `start` if that doesnt exist:

```json
{
  "name": "my-cool-server",
  "scripts": {
    "start": "node server.js",
    "start-production": "taco-nginx node server.js"
  }
}
```

then you just pack up your app and pipe the tarball to your server somehow:

```
$ taco-pack . | webcat maxogden
```

on server:

```
$ webcat maxogden | taco-build "npm install --production" | taco-deploy-mongroup .
```
