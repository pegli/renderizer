# renderizer

Renderizer is a Titanium build plugin which can automate rendering of image
resources at different resolutions for different platforms.  It reads in a
YAML config file which specifies output directories, DPIs, and lists of images
to render.

Included is a simple applescript for automating Adobe Illustrator.  Renderizer
is capable of using either Inkscape or Illustrator as the render backend.

It is assumed that your Illustrator files were created with a DPI of 72.  The
scaling property given to Illustrator assumes this is the case; if it isn't,
either edit the illustrator-render script or edit your images.

Renderizer will look for an `images.yaml` file in your project directory (ie,
next to the Resources and plugins folders).  It looks like this:

```yaml
icons:
   backend: illustrator

   output:
      - path: Resources/images/ipod
        dpi: 72

      - path: Resources/images/ipod
        dpi: 144
        append: '@2x'

      - path: Resources/images/ipad
        dpi: 82

   images:
      - icons/foo.ai
      - icons/bar.ai
      - icons/baz.ai
      - icons/foobar.ai

androidui:
   backend: illustrator

   output:
      - path: Resources/images/android
        dpi: 90

   images:
      - navbar.ai
      - background.ai
```

Images are assumed to be in an `images` directory in your project directory.

To install the plugin, make a `plugins` directory in your project directory.
Then:

```sh
git clone git@github.com:russfrank/renderizer.git
```

Then, add to your `<plugins>` section in your `tiapp.xml`:

```xml
<plugins>
   <plugin version="0.0">renderizer</plugin>
</plugins>
```

Now, your images will be rendered whenever you build your project.  Images are
only re-rendered when their modification date has changed.  So, touch an image
source if you need it re-rendered.
