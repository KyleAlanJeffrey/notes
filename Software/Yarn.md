Yet Another Resource


### Yarn Workspaces.
tutorial: https://www.youtube.com/watch?v=G8KXFWftCg0

*Workspaces are a new way to set up your package architecture that’s available by default starting from Yarn 1.0. It allows you to setup multiple packages in such a way that you only need to run `yarn install` once to install all of them in a single pass.*

### [How to use it? ](https://classic.yarnpkg.com/lang/en/docs/workspaces/#toc-how-to-use-it)

Add the following in a `package.json` file. Starting from now on, we’ll call this directory the “workspace root”:

**package.json**

```
{
  "private": true,
  "workspaces": ["workspace-a", "workspace-b"]
}
```
Note that the `private: true` is required! Workspaces are not meant to be published, so we’ve added this safety measure to make sure that nothing can accidentally expose them.

After this file has been created, create two new subfolders named `workspace-a` and `workspace-b`. In each of them, create another `package.json` file with the following content:

**workspace-a/package.json:**

```
{
  "name": "workspace-a",
  "version": "1.0.0",

  "dependencies": {
    "cross-env": "5.0.5"
  }
}
```

**workspace-b/package.json:**

```
{
  "name": "workspace-b",
  "version": "1.0.0",

  "dependencies": {
    "cross-env": "5.0.5",
    "workspace-a": "1.0.0"
  }
}
```

Finally, run `yarn install` somewhere, ideally inside the workspace root. If everything works well, you should now have a similar file hierarchy:

```
/package.json
/yarn.lock

/node_modules
/node_modules/cross-env
/node_modules/workspace-a -> /workspace-a

/workspace-a/package.json
/workspace-b/package.json
```


**The gist of what the workspace does is symlink the code from workspace into a node_modules package.**