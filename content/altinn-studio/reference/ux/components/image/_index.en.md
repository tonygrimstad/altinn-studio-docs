---
title: Image
description: Display visual content such as pictures, screenshots, illustrations, or graphics
toc: true
schemaname: Image
weight: 10
aliases:
- /altinn-studio/reference/ux/images/
- /altinn-studio/reference/ux/components/images
- /altinn-studio/guides/design/guidelines/components/picture-component/
---

---
## Usage

Use images and illustrations to emphasize points or illustrate concepts that are difficult to explain using text.

### Anatomy
![Example image and alt text anatomy](image-and-alt-text-en.png)

{{%  anatomy-list %}}
1. **Image**: Photo, screenshot, illustration, or graphic.
2. **Alternative text**: Used by screen readers and displayed if the image can not be rendered.
{{% /anatomy-list %}}

### Best practices
We recommend following the guidelines by [UUtilsynet](https://www.uutilsynet.no/regelverk/bilder-og-grafikk/205).

- Add an alternative text which explains the image. The alt. text will be displayed if the image is unavailable and is used by screen readers.
- If an image is purely decorative, it's best not to include an alternative text.
- Don't use images for image's sake. Ask yourself if the image illustrates a point or increases the understanding of what you are trying to tell.
- Check if the image scales well on devices like mobile or tablet. An image which looks good on a PC can quickly fill a smaller screen.
- Avoid using images instead of text, as screen readers cannot read it.

### Content guidelines

Keep alternative texts consistent:
- Never start with "Image of ..."
- Write short and start with the most essential part of the image.
- End by saying if the photo is an illustration or graphic.

<br>

**Example** 

<img src="https://www.uutilsynet.no/sites/tilsyn/files/styles/xxl/public/2023-01/Tretralle.png?itok=gBevDs0F" alt="Old wooden trolley. Photograph." width="300px"/>

Alt text: "Old wooden trolley. Photograph."

<br>

For more guidelines and examples, see [UUtilsynet](https://www.uutilsynet.no/regelverk/bilder-og-grafikk/205).

## Properties

The following is an autogenerated list of the properties available for {{% title %}} based on the component's JSON schema file (linked below).

{{% notice warning %}}
We are currently updating how we implement components, and the list of properties may not be entirely accurate.
{{% /notice %}}

{{% component-props %}}

## Configuration

{{% notice warning %}}
We are currently updating Altinn Studio Designer with more configuration options!
 We'll update the documentation to reflect the new changes once they are stable.
  In the meantime, there may be more options available in beta mode.
{{% /notice %}}

### Add component

{{<content-version-selector classes="border-box">}}
{{<content-version-container version-label="Altinn Studio Designer">}}

You can add a component in [Altinn Studio Designer](/altinn-studio/getting-started/) by dragging it from the list of components to the page area.
Selecting the component brings up its configuration panel.

{{</content-version-container>}}
{{<content-version-container version-label="Code">}}

Basic image component:

{{< code-title >}}
App/ui/layouts/{page}.json
{{< /code-title >}}

```json{hl_lines="6-14"}
{
  "$schema": "https://altinncdn.no/toolkits/altinn-app-frontend/4/schemas/json/layout/layout.schema.v1.json",
  {
    "data": {
      "layout": [
        {
          "id": "komponent-id",
          "type": "Image",
          "image": {
            "src": {},
             "width": "100%",
             "align": "center"
            }
        }
      ]
    }
  }
}
```

{{</content-version-container>}}
{{</content-version-selector>}}

### Alternative text (`textResourceBindings.altTextImg`)

{{<content-version-selector classes="border-box">}}
{{<content-version-container version-label="Altinn Studio Designer">}}

Choose 'Alternativ tekst for bilde' in the drop-down menu.

![Settings add text](innstilling-tekst.png)

Click the plus sign to create a new text or the magnifying glass to pick an existing [text resource](/altinn-studio/reference/ux/texts/#add-and-change-texts-in-an-application).

![Settings for alternative text](innstilling-alternativ-tekst.png)

{{</content-version-container>}}
{{<content-version-container version-label="Code">}}

Corresponding settings in the page's JSON file.

{{< code-title >}}
App/ui/layouts/{page}.json
{{< /code-title >}}

```json{hl_lines="7-9"}
{
  "data": {
    "layout": [
      {
        "id": "kommune-logo",
        "type": "Image",
        "textResourceBindings": {
          "altTextImg": ""
        },
        ...
      }
    ]
  }
}
```

{{</content-version-container>}}
{{</content-version-selector>}}

### Image settings (`image`)

#### Image source (`image.src`)

The default source is `nb`; any language that does not define a separate image source will use this source.
  List another language code and image source to add a source, as in the example below.

Available language sources are `en` (English), `nb` (Norwegian Bokmål), and `nn` (Norwegian Nynorsk).


{{<content-version-selector classes="border-box">}}
{{<content-version-container version-label="Altinn Studio Designer">}}

![Settings for source](innstilling-kilde.png)

{{</content-version-container>}}
{{<content-version-container version-label="Code">}}

{{< code-title >}}
App/ui/layouts/{page}.json
{{< /code-title >}}

```json{hl_lines=["5-8"]}
{
  "id": "kommune-logo",
  "type": "Image",
  "image": {
    "src": {
      "nb": "/testdep/flyttemelding-sogndal/kommune-logo.png",
      "nn": "wwwroot/kommune-logo.png"
    },
    ...
  }
}
```
{{</content-version-container>}}
{{</content-version-selector>}}

The image source may be external or local to the app.

For external images, the source is the *image URL* (e.g. `https://examples.com/myImage.png`).

To host an image in the application, place it in the folder `App/wwwroot` (if the folder does not exist, you can create it).
 Static hosting must be [configured manually](#configure-static-hosting) for apps created before December 2021.

An image placed in `App/wwwroot` can be referenced in the following ways:
- Using its *relative URL*: `/<org or username>/<app-name>/image.png` or
- Using the *image path*: `wwwroot/image.png`. The path will resolve to the image's relative URL before the image is loaded.

#### Configure static hosting
For apps created *before December 2021*, static hosting must be configured manually by adding the line
 `app.UseStaticFiles('/' + applicationId);` in the `Configure` method in `App/Program.cs` as shown below:

{{< code-title >}}
App/Program.cs
{{< /code-title >}}

```C# {hl_lines="5"}
void Configure()
  {
    ...
    app.UseRouting();
    app.UseStaticFiles('/' + applicationId);
    app.UseAuthentication();
    ...
  }
```

`applicationId` is the same as `id`  in `App/configApplicationmetadata.json`.

#### Width and alignment (`image.width`, `image.align`)

By using `width`, you can adjust the image size by specifying the width of the image in percentage.
 The height is automatically set to maintain proportions. The default setting is 100% (original width).

The property `align` controls the horizontal position of the image relative to the container.

{{<content-version-selector classes="border-box">}}
{{<content-version-container version-label="Altinn Studio Designer">}}

![Settings for width and alignment](innstilling-bredde-plassering.png)

{{</content-version-container>}}
{{<content-version-container version-label="Code">}}

{{< code-title >}}
App/ui/layouts/{page}.json
{{< /code-title >}}

```json{hl_lines="14-15"}
{
  "data": {
    "layout": [
      {
        "id": "kommune-logo",
        "type": "Image",
        "textResourceBindings": {
          "altTextImg": "kommune-logo.altTextImg"
        },
        "image": {
          "src": {
            "nb": "wwwroot/kommune-logo.png",
          },
          "width": "100%",
          "align": "center"
        }
      }
    ]
  }
}
```
{{</content-version-container>}}
{{</content-version-selector>}}

The following options are available for positioning:

- `flex-start`: Left-aligned
- `center`: Centered
- `flex-end`: Right-aligned
- `space-between`: The elements are evenly distributed horizontally, with equal spacing between each element and no spacing at the start and end.
- `space-around`: The elements are evenly distributed horizontally with equal spacing between each element, including spacing at the start and end, which is half the spacing between the elements.
- `space-evenly`: The elements are evenly distributed horizontally with equal spacing between each element, including at the start and end, so that the total spacing is evenly distributed.

{{< property-docs prop="renderAsSummary" >}}

{{< property-docs prop="hidden" >}}

{{< property-docs prop="page-break" >}}

{{< property-docs prop="grid-short" >}}

<!-- ## Examples -->