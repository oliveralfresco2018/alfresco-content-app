### Publishing library to NPM

Before you publish you should always rebuild the library:

```sh
npm run build:my-extension
```

Go to the output folder and run the publish command.

```sh
cd dist/my-extension
npm publish
```

Note, you are required to have a valid [NPM](https://www.npmjs.com/) account.

<p class="tip">
See more details in the [Publishing your library](https://github.com/angular/angular-cli/wiki/stories-create-library#publishing-your-library) article.
</p>