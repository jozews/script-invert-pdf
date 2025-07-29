
    #!/usr/bin/env python3
    
    
    import sys
    from pdf2image import convert_from_path
    
    
    path = sys.argv[1]
    images = convert_from_path(path)
    
    for index_image, image in enumerate(images):
    
        rgbs = image.getdata()
        rgbs_inverse = []
    
        for rgb in rgbs:
            rgb_inverse = tuple(map(lambda value: abs(value - 255), rgb))
            rgbs_inverse.append(rgb_inverse)
    
        image.putdata(rgbs_inverse)
        images[index_image] = image
        
    images[0].save(path, "PDF", resolution = 100.0, save_all = True, append_images = images[1 : ])


Convert pdf into night mode. Run twice to get original color.


Place _invert_pdf_ in your path and run

    invert_pdf path/to/pdf.pdf
