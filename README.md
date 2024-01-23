# DeOldify Image Colorization

## Overview

DeOldify is an advanced deep learning application that colorizes black and white images using neural networks. This repository contains a Python script to set up and use DeOldify for image colorization. The script enables users to colorize images sourced from URLs, offering options to adjust colorization quality and watermark presence.

## Prerequisites

- Python 3.x
- Git
- Access to a GPU (highly recommended for faster processing)
- Basic understanding of Python and Jupyter Notebooks

## Installation

1. **Clone the Repository:**
   ```
   git clone https://github.com/jantic/DeOldify.git
   cd DeOldify
   ```

2. **Install Dependencies:**
   ```
   pip install -r requirements-colab.txt
   ```

3. **Download Pre-trained Model:**
   ```
   mkdir 'models'
   wget https://data.deepai.org/deoldify/ColorizeArtistic_gen.pth -O ./models/ColorizeArtistic_gen.pth
   ```

## Usage

1. **Import Required Modules:**
   ```python
   from deoldify import device
   from deoldify.device_id import DeviceId
   import torch
   from deoldify.visualize import *
   import warnings
   ```

2. **Check for GPU Availability:**
   ```python
   device.set(device=DeviceId.GPU0)
   if not torch.cuda.is_available():
       print('GPU not available.')
   ```

3. **Suppress Warnings:**
   ```python
   warnings.filterwarnings("ignore", category=UserWarning, message=".*?Your .*? set is empty.*?")
   ```

4. **Initialize the Colorizer:**
   ```python
   colorizer = get_image_colorizer(artistic=True)
   ```

5. **Colorize an Image from URL:**
   - Set the `source_url` variable to the image URL.
   - Adjust `render_factor` (7 to 40) for colorization quality.
   - Set `watermarked` to `True` or `False`.

   ```python
   source_url = 'https://i.imgur.com/hOiL2uT.jpg'  # Replace with your image URL
   render_factor = 40  # Adjust the render factor as needed
   watermarked = True  # Set to False if watermark is not needed

   if source_url is not None and source_url != '':
       image_path = colorizer.plot_transformed_image_from_url(url=source_url, render_factor=render_factor, compare=True, watermarked=watermarked)
       show_image_in_notebook(image_path)
   else:
       print('Provide an image URL and try again.')
   ```

## Contributing

Contributions to this project are welcome. Please fork the repository and submit a pull request with your proposed changes.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
