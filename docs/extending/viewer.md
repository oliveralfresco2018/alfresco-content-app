### Viewer

Viewer component in ACA supports the following extension points:

- Content Viewers
- Toolbar actions
- `More` toolbar actions
- `Open With` actions

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "viewer": {
      "content": [],
      "toolbarActions:": [],
      "toolbarMoreMenu:": [],
      "openWith": []
    }
  }
}
```

#### Content View

You can provide custom components that render a particular type of the content based on extensions.

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "viewer": {
      "content": [
        {
          "id": "app.viewer.pdf",
          "fileExtension": "pdf",
          "component": "app.components.tabs.metadata"
        },
        {
          "id": "app.viewer.docx",
          "fileExtension": "docx",
          "component": "app.components.tabs.comments"
        }
      ]
    }
  }
}
```

In the example above we replace `PDF` view with the `metadata` tab
and `DOCX` view with the `comments` tab.

Every custom component receives the following properties at runtime:

| Name      | Type                   | Description                 |
| --------- | ---------------------- | --------------------------- |
| node      | MinimalNodeEntryEntity | Node entry to be displayed. |
| url       | string                 | File content URL.           |
| extension | string                 | File name extension.        |

#### Toolbar actions

The default toolbar actions from the ACA viewer can be customized through extensions to be replaced, modified or disabled.
New viewer toolbar actions can also be added from the extensions config:

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "viewer": {
      "toolbarActions": [
        {
          "id": "app.viewer.versions",
          "order": 500,
          "title": "APP.ACTIONS.VERSIONS",
          "icon": "history",
          "actions": {
            "click": "MANAGE_VERSIONS"
          },
          "rules": {
            "visible": "app.toolbar.versions"
          }
        }
      ],
      "toolbarMoreMenu": [...]
    }
  }
}
```

The ADF Viewer component allows you to provide custom entries for the `More` menu button on the toolbar.
The ACA provides an extension point for this menu that you can utilize to populate custom menu items:

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "viewer": {
      "toolbarActions": [...],
      "toolbarMoreMenu": [
        {
          "id": "app.viewer.share",
          "order": 300,
          "title": "Share",
          "icon": "share",
          "actions": {
            "click": "SHARE_NODE"
          },
          "rules": {
            "visible": "app.selection.file.canShare"
          }
        }
      ]
    }
  }
}
```

#### Open With actions

You can provide a list of `Open With` actions to render with every instance of the Viewer.

In the following example, we create a simple `Snackbar` action reference,
and invoke it from the custom `Open With` menu entry called `Snackbar`.

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "actions": [
    {
      "id": "plugin1.actions.info",
      "type": "SNACKBAR_INFO",
      "payload": "I'm a nice little popup raised by extension."
    }
  ],

  "features": {
    "viewer": {
      "openWith": [
        {
          "id": "plugin1.viewer.openWith.action1",
          "type": "button",
          "icon": "build",
          "title": "Snackbar",
          "actions": {
            "click": "plugin1.actions.info"
          }
        }
      ]
    }
  }
}
```

As with other content actions, custom plugins can disable, update or extend `Open With` actions.