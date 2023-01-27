## How to publish to npm ##
Make sure `package.json` contains correct information
- Remove any dependencies that you are not using from the file
- After they are removed, use `npm prune` to remove them from your `node_modules`

**The three main things that need to be filled out in `package.json`**
- Change `name` of package if needed
- Change `version` of package if needed
- Make sure `main` is pointing to your main file
  - Make sure your is referncing the transpiled versions of your source code (if you have them)

When ready:
```npm publish --access public```

### If you are not logged in... ###
- Use `npm login`. When prompted, enter login info
- If you don't have an account, use `npm adduser` to create one. Enter info when prompted
