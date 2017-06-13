## Picture Resizing Script ##
## Author: Yoel Casal
## Aim: This script facilitates image resizing on large scale with a canvas expansion option

# Load libraries
from PIL import Image
import glob
import math

# Point folder
folderJPG = #'Your folder with JPG images'
folderPNG = #'Your folder with PNG images'

# Aggregate files into directory
directory = glob.glob(folderPNG) + glob.glob(folderJPG)

# Write new files to:
write_to = #'Your output folder'

# Introduce a function to resize different images to a standard
def resize(dir = directory, image_width = None, image_height = None, resize_canvas = 'FALSE'):
        
    # Loop resizing over all images
        for fname in dir:
            img = Image.open(fname) # image extension *.png,*.jpg
            
            # Convert to RGBA
            img = img.convert("RGBA")

            # Make dummies
            new_width = image_width
            new_height = image_height
            
            # Define old sizes
            old_width, old_height = img.size
    
            # Define new sizes 
            if image_height == None and image_width == None:
                raise ValueError('Please provide width and/or height')
    
            elif image_height != None and image_width != None:
                new_width = image_width
                new_height = image_height
                
            elif image_height == None and image_width != None:
                new_height = image_width * old_height / old_width
                
            elif image_height != None and image_width == None:
                new_width  = image_height * old_width / old_height
    
            # Resize the picture
            img = img.resize((int(new_width), int(new_height)), Image.ANTIALIAS)
            
            #  Output name
            output_name = fname.rsplit('\\', 1)[-1]

            # Check if canvas needs to be resized + if so, apply transformation
            if resize_canvas == 'TRUE':
                # Duplicate img
                im = img
                # Select max(height, width)
                canvas = max(int(new_width), int(new_height))           
                
                # Center the image
                x1 = int(math.floor((canvas - new_width) / 2))
                y1 = int(math.floor((canvas - new_height) / 2))
                
                mode = im.mode
                new_background = (255, 255, 255, 0)
                
                img = Image.new(mode, (canvas, canvas), new_background)
                img.paste(im, (x1, y1, x1 + int(new_width), y1 + int(new_height)))
                img.save(write_to + output_name)
            
            else:
                img.save(write_to + output_name)
                
                
# Apply function
# Providing height and width will force an image into those dimensions
# Providing only a height will scale width automatically and maintain scale ratio
# Providing only a width will scale height automatically and maintain scale ratio
# Canvas resizing will resize the canvas to the largest, being height or width
resize(dir = directory, image_width = 132, image_height = None, resize_canvas = 'TRUE')
        
# Drop directory
directory = []
