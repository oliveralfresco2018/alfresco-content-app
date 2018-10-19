### Consuming extension library

Assuming you have published your extension library to NPM, you can install it using the standard command:

```sh
npm install my-extension
```

This installs the library and all its dependencies.

<p class="warning">
You do not need to install the library in the original workspace as the application is already configured to use the local version from the `dist` folder.
</p>

#### Copy assets

Edit the `angular.json` configuration file and add the following rule if you develop and test extension libraries in the same workspace.

```json
{
  "glob": "**/*.json",
  "input": "dist/my-extension/assets",
  "output": "/assets/plugins"
}
```

Use the following rule if you are installing an extension from NPM:

```json
{
  "glob": "**/*.json",
  "input": "node_modules/my-extension/assets",
  "output": "/assets/plugins"
}
```

#### Register module

In the main application, edit the `src/app/extensions.module.ts` file and append the module declaration as in the next example:

```typescript
...
import { MyExtensionModule } from 'my-extension';

@NgModule({
    ...
    imports: [
        ...,
        MyExtensionModule
    ]
})
export class AppExtensionsModule {}
```

#### Register plugin

Finally, update the `assets/app.extensions.json` file and add a reference to the new plugin:

```json
{
    "$references": [
        ...,
        "my-extension.json"
    ]
}
```