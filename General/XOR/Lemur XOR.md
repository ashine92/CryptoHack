# Lemur XOR

```python
$ gmic flag.png lemur.png -blend xor -o result.png
[gmic]-0./ Start G'MIC interpreter.
[gmic]-0./ Input file 'flag.png' at position 0 (1 image 582x327x1x3).
[gmic]-1./ Input file 'lemur.png' at position 1 (1 image 582x327x1x3).
[gmic]-2./ Blend all images [0,1] together, using 'xor' mode and opacity 1.
[gmic]-1./ Output image [0] as png file 'result.png' (1 image 582x327x1x3).
[gmic]-1./ End G'MIC interpreter.
```

Mở file result.png:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/85258bfe-e770-46e2-b776-c6ac8484abe5/17d33b9d-3339-4f8a-a10e-27b933b7e70e/Untitled.png)

# Another Solution

```python
#!/usr/bin/env python3

from PIL import Image

lemur = Image.open("lemur.png")
flag = Image.open("flag.png")

pixels_lemur = lemur.load() # create the pixel map
pixels_flag = flag.load()

for i in range(lemur.size[0]): # for every pixel:
    for j in range(lemur.size[1]):
        # Gather each pixel
        l = pixels_lemur[i,j]
        f = pixels_flag[i,j]

        # XOR each part of the pixel tuple
        r = l[0] ^ f[0]
        g = l[1] ^ f[1]
        b = l[2] ^ f[2]

        # Store the resulatant tuple back into an image
        pixels_flag[i,j] = (r, g, b)

flag.save("lemur_xor_flag.png")
```
