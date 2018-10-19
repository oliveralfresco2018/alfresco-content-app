### Content metadata presets

The content metadata presets are needed by the [Content Metadata Component](https://alfresco.github.io/adf-component-catalog/components/ContentMetadataComponent.html#readme) to render the properties of metadata aspects for a given node. 
The different aspects and their properties are configured in the `app.config.json` file, but they can also be set on runtime through extension files.

Configuring these presets from `app.extensions.json` will overwrite the default application setting. 
Settings them from custom plugins allows user to disable, update or extend these presets.
Check out more info about merging extensions [here](#merging-properties).

The `content-metadata-presets` elements can be switched off by setting the `disabled` property.
This can be applied also for nested items, allowing disabling down to aspect level. 

<p class="tip">
In order to modify or disable existing entries, you need to know the id of the target element, along with its parents ids.
</p>

Your extensions can perform the following actions at runtime:
* Add new presets items.
* Add new items to existing presets at any level.
* Disable specific items down to the aspect level.
* Modify any existing item based on id.  

Regarding properties, you can either:
 * Add new properties to existing aspect, or 
 * Redefine the properties of an aspect. 
 
Review this code snippet to see how you can overwrite the properties for `exif:exif` aspect from an external plugin:
```json
  {
     "$schema": "../../../extension.schema.json",
     "$version": "1.0.0",
     "$name": "plugin1",

     "features": {
       "content-metadata-presets": [
         {
           "id": "app.content.metadata.custom",
           "custom": [
             {
               "id": "app.content.metadata.customGroup",
               "items": [
                 {
                   "id": "app.content.metadata.exifAspect",
                   "disabled": true
                 },
                 {
                   "id": "app.content.metadata.exifAspect2",
                   "aspect": "exif:exif",
                   "properties": [
                     "exif:orientation",
                     "exif:manufacturer",
                     "exif:model",
                     "exif:software"
                   ]
                 }
               ]
             }
           ]
         }
       ]
     }
   }
``` 
This external plugin disables the initial `exif:exif` aspect already defined in the `app.extensions.json` and defines other properties for the `exif:exif` aspect. 
Here is the initial setting from `app.extension.json`:
```json
...
    "content-metadata-presets": [
      {
        "id": "app.content.metadata.custom",
        "custom": [
          {
            "id": "app.content.metadata.customGroup",
            "title": "APP.CONTENT_METADATA.EXIF_GROUP_TITLE",
            "items": [
              {
                "id": "app.content.metadata.exifAspect",
                "aspect": "exif:exif",
                "properties": [
                  "exif:pixelXDimension",
                  "exif:pixelYDimension",
                  "exif:dateTimeOriginal",
                  "exif:exposureTime",
                  "exif:fNumber",
                  "exif:flash",
                  "exif:focalLength",
                  "exif:isoSpeedRatings",
                  "exif:orientation",
                  "exif:manufacturer",
                  "exif:model",
                  "exif:software"
                ]
              }
            ]
          }
        ]
      }
    ]
...

``` 
<p class="tip">
In order to allow the content-metadata presets to be extended, the settings from `app.config.json` must be copied to the `app.extensions.json` file and its ids must be added to all the items.
Having ids allows external plugins to extend the current setting.
</p>
