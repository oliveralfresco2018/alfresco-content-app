### Content Actions

Most of the UI elements that operate with content, like toolbar buttons or menus,
are based on `ContentActionRef` interface implementation:

```ts
interface ContentActionRef {
  id: string;
  type: ContentActionType;

  title?: string;
  description?: string;
  order?: number;
  icon?: string;
  disabled?: boolean;
  children?: Array<ContentActionRef>;
  component?: string;
  actions?: {
    click?: string;
    [key: string]: string;
  };
  rules?: {
    enabled?: string;
    visible?: string;
    [key: string]: string;
  };
}
```

You can define content actions in the `app.extensions.json` file using the structure above.