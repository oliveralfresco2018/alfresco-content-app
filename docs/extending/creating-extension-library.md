### Creating extension library

First, generate a new project within the workspace:

```sh
ng generate library my-extension
```

You will get a new project in the `projects/my-extensions` folder.
By default, the project contains at least the following content:

- Example component `my-extension.component.ts`
- Example service `my-extension.service.ts`
- Angular Module example `my-extension.module.ts`

Next, build the project with the following command:

```sh
ng build my-extension
```

Angular CLI automatically configures Typescript path mappings for the project, so that you do not need any additional steps to link the library.

#### Register dynamic components

Update `my-extension.module.ts` and put all the content you plan to use at runtime dynamically to the `entryComponents` section of the module.

```typescript
@NgModule({
  imports: [],
  declarations: [MyExtensionComponent],
  exports: [MyExtensionComponent],
  entryComponents: [MyExtensionComponent]
})
export class MyExtensionModule {}
```

Now we need to register `MyExtensionComponent` as an extension component.
Update the code as in the next example:

```typescript
import { ExtensionService } from '@alfresco/adf-extensions';

@NgModule({...})
export class MyExtensionModule {
    constructor(extensions: ExtensionService) {
        extensions.setComponents({
            'my-extension.main.component': MyExtensionComponent,
        });
    }
}
```

Now you can use the `my-extension.main.component` identifier in the JSON definitions
if you want to reference the `MyExtensionComponent`.

#### Plugin definition file

Create a new `assets/my-extension.json` file in the library project root folder with the following content:

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",
  "$description": "demo plugin",

  "routes": [
    {
      "id": "my.extension.route",
      "path": "ext/my/route",
      "component": "my-extension.main.component"
    }
  ],

  "features": {
    "navbar": [
      {
        "id": "my.extension.nav",
        "items": [
          {
            "id": "my.extension.main",
            "icon": "extension",
            "title": "My Extension",
            "route": "my.extension.route"
          }
        ]
      }
    ]
  }
}
```

Update the root `package.json` file and append the following entry to the `scripts` section:

```json
{
    "scripts": {
        ...,

        "build:my-extension":
            "ng build my-extension && cpr projects/my-extension/assets dist/my-extension/assets --deleteFirst"
    }
}
```

You can now use that script to build the library and copy assets to the output folder.

<p class="tip">
It is good practice to provide installation instructions for your library in the `README.md` file.
Be sure to mention that developers should have a build rule to copy your plugin definition file to the `assets/plugins` folder of the main application.
</p>