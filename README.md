
```
#!/usr/bin/env python3


import sys
from pdf2image import convert_from_path


path = sys.argv.pop(1) if len(sys.argv) > 1 else "../Documents/scores/beethoven-11.pdf"
images = convert_from_path(path)
print(f"Found {len(images)} images in {path}...")

for index_image, image in enumerate(images):

    rgbs = image.getdata()
    rgbs_inverse = []

    for rgb in rgbs:
        rgb_inverse = tuple(map(lambda value: abs(value - 255), rgb))
        rgbs_inverse.append(rgb_inverse)

    image.putdata(rgbs_inverse)
    images[index_image] = image
    print(f"Processed image {index_image + 1} of {len(images)}...")
    
print(f"Saving {len(images)} images to {path}...")
images[0].save(path, "PDF", resolution = 100.0, save_all = True, append_images = images[1 : ])
```
