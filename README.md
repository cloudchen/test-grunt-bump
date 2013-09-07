How to use grunt-bump task
===============

## When is appropriate time to run `grunt bump` task?
In general, you should run it when **code is ready for release** and **working directory is clean**

## What does `grunt bump` do?
By default, it

1. **bumps** patch verion number within `package.json` file
2. **commits** being changed `package.json` file to local git repository
3. **creates tag** by using bumped version number to local git repository
4. **pushes** local changes to remote branch


## Key configurations
### Add repository url definition in `package.json` file

```json
{
  "repository": {
    "type": "git",
    "url": "https://github.com/cloudchen/test-grunt-bump.git"
  }
}
```

Let `grunt bump` task know where upstream is.
This can also be used to avoid warnning with `npm install` or `npm update`

### Override `Gruntfile.js` default upstream by reading corresponding configuration from `package.json`

```js
grunt.initConfig({
  pkg: grunt.file.readJSON('package.json'),
  ...
  bump: {
    options: {
      pushTo: '<%=pkg.repository.url%>'
    }
  }
  ...
});
```

### Disable `git-push` functionality in `Gruntfile.js`

```js
grunt.initConfig({
  pkg: grunt.file.readJSON('package.json'),
  ...
  bump: {
    options: {
      push: false,
      pushTo: '<%=pkg.repository.url%>'
    }
  }
  ...
});
```

## Other tasks

### Bump patch version number, from 0.0.1 to 0.0.2
```sh
grunt bump:patch
# equals to
grunt bump
```
### Bump minor version number, from 0.0.1 to 0.1.0
```sh
grunt bump:minor
```

### Bump major version number, from 0.1.0 to 1.0.0
```sh
grunt bump:major
```
