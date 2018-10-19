### Sidebar (Info Drawer)

You can provide the following customizations for the Sidebar (aka Info Drawer) component:

- Add extra tabs with custom components
- Disable tabs from the main application or extensions
- Replace content or properties of existing tabs

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "sidebar": [
      {
        "id": "app.sidebar.properties",
        "order": 100,
        "title": "Properties",
        "component": "app.components.tabs.metadata"
      },
      {
        "id": "app.sidebar.comments",
        "order": 200,
        "title": "Comments",
        "component": "app.components.tabs.comments"
      }
    ]
  }
}
```

The example above renders two tabs:

- `Properties` tab that references the `app.components.tabs.metadata` component
- `Comments` tab that references the `app.components.tabs.comments` component

All corresponding components must be registered for runtime use.

<p class="tip">
See the [Registration](#registration) section for more details
on how to register your own entries to be re-used at runtime.
</p>
#### Tab properties

| Name          | Description                                                 |
| ------------- | ----------------------------------------------------------- |
| **id**        | Unique identifier.                                          |
| **component** | The main [component](#components) to use for the route.     |
| **title**     | Tab title or resource key.                                  |
| icon          | Tab icon                                                    |
| disabled      | Toggles disabled state. Can be assigned from other plugins. |
| order         | The order of the element.                                   |

#### Tab components

Every component you assign for the tab content receives the following additional properties at runtime:

| Name | Type                   | Description                 |
| ---- | ---------------------- | --------------------------- |
| node | MinimalNodeEntryEntity | Node entry to be displayed. |

### Toolbar

The toolbar extension point is represented by an array of Content Action references.

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "toolbar": [
      {
        "id": "app.toolbar.preview",
        "title": "View",
        "icon": "open_in_browser",
        "actions": {
          "click": "VIEW_FILE"
        },
        "rules": {
          "visible": "app.toolbar.canViewFile"
        }
      },
      {
        "id": "app.toolbar.download",
        "title": "Download",
        "icon": "get_app",
        "actions": {
          "click": "DOWNLOAD_NODES"
        },
        "rules": {
          "visible": "app.toolbar.canDownload"
        }
      }
    ]
  }
}
```

The content actions are applied to the toolbars for the following Views:

- Personal Files
- Libraries
- Shared
- Recent Files
- Favorites
- Trash
- Search Results