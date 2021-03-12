# Parcel server and cache issue

https://github.com/parcel-bundler/parcel/issues/5989

## Steps to recreate

1. Install dependencies `yarn install`
2. Run the dev server `yarn start`
3. Change the line in `included.styl` to be `awesome-color = blue`

Expected: the page hot reloads to a blue page.
Actual: it remains red.

4. Append a // to the end of main.styl so that it looks like this:
```
html
  background awesome-color //

```

5. Notice the page reloads blue.
6. Delete the ` //` from main.styl

Expected: The page remains blue.
Actual: The page hot reloads and becomes red.

My guess is this is serving a cached compilation based on the hashes of the contents of the stylus files in the dependency tree. I also guess that my includes.styl doesn't live in that dependency tree.
