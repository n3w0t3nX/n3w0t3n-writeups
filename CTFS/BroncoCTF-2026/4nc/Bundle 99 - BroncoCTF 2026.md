
## Challenge Description

> Yoshie found this random file lying around.
>
> Apparently someone said it's the **99th bundle of brushes**.
>
> What is that supposed to mean...
>
> **P.S.** This challenge can be solved without installing any software, but you'll have to find an online way to load the bundle.

---

The challenge provides a single file called `Bundle_99`.

I had no idea what it was, so I started with the `file` command.

```bash
file Bundle_99
```

Output:

```text
Bundle_99: Zip data (MIME type "application/x-krita-resourcebundle")
```

So it's just a ZIP archive.

I extracted it.

```bash
unzip Bundle_99
```

```text
Archive: Bundle_99

extracting: mimetype
inflating: paintoppresets/Brush 99.kpp
inflating: preview.png
inflating: META-INF/manifest.xml
inflating: meta.xml
```

At first, I expected to find the flag inside one of the XML files, but there was nothing useful.

The interesting part was the MIME type:

```text
application/x-krita-resourcebundle
```

After a little research, I found that this is a **Krita Resource Bundle**, which contains custom brushes for the Krita drawing application.

![[cff4fcf3ab8968828f497c61a72c935c.jpg]]

So I installed Krita and created a new project.

Now we need to import the brush contained in:

```text
paintoppresets/Brush 99.kpp
```

Open:

```text
Settings → Manage Resources...
```

Then import the brush preset.

![[import.png]]

Select the extracted brush file.

![[brush.png]]

After importing it, select **Brush 99** from the brush presets.

![[add brush.png]]

Now simply draw anywhere on the canvas.

Instead of a normal brush stroke, it paints the flag directly.

![[flag.png]]

### Flag

```text
bronco{1m4n4rt15ttru5t}
```
