### Navigation Bar

The Navigation bar consists of Link elements (`NavBarLinkRef`) organized into Groups (`NavBarGroupRef`).

```ts
export interface NavBarGroupRef {
  id: string;
  items: Array<NavBarLinkRef>;

  order?: number;
  disabled?: boolean;
}

export interface NavBarLinkRef {
  id: string;
  icon: string;
  title: string;
  route: string;

  url?: string; // evaluated at runtime based on route ref
  description?: string;
  order?: number;
  disabled?: boolean;
}
```

Your extensions can perform the following actions at runtime:

- Register new groups with links
- Insert new links into existing groups
- Update properties of the existing links
- Disable existing links or entire groups

```json
{
  "$schema": "../../../extension.schema.json",
  "$version": "1.0.0",
  "$name": "plugin1",

  "features": {
    "navbar": [
      {
        "id": "app.navbar.primary",
        "items": [
          {
            "id": "app.navbar.personalFiles",
            "icon": "folder",
            "title": "Personal Files",
            "route": "personal-files"
          },
          {
            "id": "app.navbar.libraries",
            "icon": "group_work",
            "title": "Libraries",
            "route": "libraries"
          }
        ]
      },
      {
        "id": "app.navbar.secondary",
        "items": [
          {
            "id": "app.navbar.shared",
            "icon": "people",
            "title": "Shared",
            "route": "shared"
          }
        ]
      }
    ]
  }
}
```