**1. Preprocessing of the captured image:**<br>
General techniques used along the processing<br>
-**Converting the image to greyscale**<br>
![image](https://github.com/Mazen030/CV-sudoku-solver/assets/93229175/6db532b5-0208-47c8-acc6-25706c89333a)<br>
Converting the Sudoku image to greyscale simplifies the information to a single intensity channel, reducing computational complexity and focusing on luminance variations.<br>
-**Applying median filter**<br>
Median filtering helps reduce noise by replacing each pixel value with the median value in its local neighborhood. This is particularly useful for smoothing the image and enhancing the visibility of Sudoku grid lines and numbers.<br>
-**Apply sharpening**<br>
Sharpening techniques enhance the edges in the image, making the Sudoku grid lines and numbers more distinct. This aids in better feature extraction and can improve the overall quality of the image.<br>
-**Applying Contrast Limited Adaptive Histogram Equalization**<br>
CLAHE is beneficial for enhancing local contrast in an image. It divides the image into small tiles and performs histogram equalization on each tile individually, preventing overamplification of noise. This can help in revealing details in both dark and bright regions.<br>
-**Gamma correction**
Gamma correction adjusts the intensity values in the image to improve its appearance on different devices. It can be applied to correct non-linearities in the display, ensuring that the Sudoku image is represented accurately.<br>
-**Applying Histogram Equalization**
Histogram Equalization is a global enhancement technique that redistributes intensity values across the entire image. While it can enhance contrast, it might amplify noise, which is why CLAHE is often preferred for Sudoku images.<br>
-**Guassian Blur**
Gaussian blur is useful for smoothing the image, reducing noise, and suppressing fine details. It can be applied as a preprocessing step to simplify the image and prepare it for subsequent processing stages.<br>
-**Thresholding**
Thresholding is employed to segment the image into binary regions (foreground and background). It is crucial for extracting the Sudoku grid and numbers from the background, aiding in subsequent image analysis and recognition tasks
We choose adaptive thresholding over global thresholding in this step. Adaptive thresholding offers superior performance as it dynamically adjusts to changes in light intensity across the image. Unlike global thresholding, which sets a single threshold for the entire image and may lead to the loss of details in areas with varying illumination, adaptive thresholding calculates different thresholds for different regions. This adaptability ensures better preservation of image information, making it the preferred choice for scenarios with uneven lighting conditions .<br>
-**Morphological operations**
They are essential components in image processing, particularly in tasks such as Sudoku image analysis. These operations involve the manipulation and analysis of the geometric structure of an image.<br>
-**Closing**:
Closing is the reverse of opening (dilation followed by erosion). It is effective in closing small gaps in the contours of objects. In Sudoku image processing, closing can help connect broken grid lines and improve the integrity of the grid structure.<br>
-**Opening followed by Closing**:
The combined application of opening and closing operations is known as the opening-closing operation.
This sequence is adept at eliminating noise and fine structures in the image while preserving the general shape and connectivity of larger structures.
It is particularly useful in scenarios where noise removal is crucial, yet the overall structure of objects needs to be retained.<br>
-**Test cases image processing differentiation** :
After converting each image to greyscale , we employ an initial differentiation among images based on their mean intensities, recognizing the necessity for individualized calibration of the constant term "c" subtracted from the weighted mean in the thresholding process. Additionally, the determination of optimal block sizes for thresholding is acknowledged as a critical hyperparameter, and a systematic tuning approach is undertaken to refine these parameters for each distinct image. This meticulous parameter tuning process ensures the adaptability of the thresholding methodology to the specific characteristics of each image, thereby enhancing the overall effectiveness of the image processing pipeline.<br>
**1.2 corners identification**
We detect contours in a binary thresholded image, identify the largest contour (assumed to be the outer frame), reorder its points, draws the reordered contour, and apply a perspective transformation to obtain a bird's-eye view.<br>
**1.3 Outer frame isolation**
After getting the right corners, we straighten the image.
It’s is likely used to obtain a "bird's-eye view" or top-down perspective of an image. This transformation is often applied to correct or alter the perspective of an image, making it appear as if it were captured from above, like a bird flying over the scene.<br>
**1.4 Grid straightening into a square** :
We used the dimensions of the binary thresholded image to calculate the size of each sub-tile, ensuring an even division of the image into a 9x9 grid.
We employed nested loops to iterate through the grid, extracting and storing each sub-tile in the number_tiles list.
We created a 9x9 subplot grid for visualization, ensuring each subplot corresponds to a sub-tile.
We iterated through the subplots, displaying each sub-tile using a grayscale colormap for better visualization to be ready to go to the OCR.<br>
**2. Phase (2)**<br>
**2.1 Basic OCR with pattern matching**
Template matching is used in various projects and applications across different domains due to its simplicity and effectiveness in certain scenarios. Here are some reasons why template matching is employed in projects:<br>
Object Detection: Template matching is commonly used for object detection in images. It helps identify instances of a specific object (template) within a larger image.
Pattern Recognition: When the pattern or object being searched for is well-defined and has a consistent appearance, template matching can be a suitable choice for recognizing and locating these patterns.<br>

OCR (Optical Character Recognition): Template matching can be used in OCR applications to locate and recognize characters or digits in images. Each character is treated as a template, and matching is performed against the input image. and many other programs<br>
Template Matching Algorithm :<br>
Template matching is used in various projects and applications across different domains due to its simplicity and effectiveness in certain scenarios. Here are some reasons why template matching is employed in projects:
Object Detection: Template matching is commonly used for object detection in images. It helps identify instances of a specific object (template) within a larger image.
Pattern Recognition: When the pattern or object being searched for is well-defined and has a consistent appearance, template matching can be a suitable choice for recognizing and locating these patterns.
OCR (Optical Character Recognition): Template matching can be used in OCR applications to locate and recognize characters or digits in images. Each character is treated as a template, and matching is performed against the input image.
How Does template matching algorithm works ?
Template matching is a technique used in image processing to locate a template (a small image or pattern) within a larger image. The process involves comparing the template with sub-regions (windows) of the larger image to find the region where the template best matches. Here's a general overview of how template matching algorithms work:<br>
**1)Select a Template**:<br>
Choose a small image or pattern that represents what you want to find in the larger image. This is your template.<br>
**2)Define a Similarity Metric**:<br>
Choose a similarity metric or a measure of how well the template matches a particular region in the larger image<br>
**3)Slide the Template**:
Move the template across the larger image by sliding it pixel by pixel or in larger steps. At each position, calculate the similarity metric for the overlapping region.<br>
**4) Find the Best Match**:<br>
Keep track of the position where the similarity metric is maximized. This position represents the location in the larger image where the template best matches.<br>
**5)Threshold or Normalize**:<br>
Optionally, apply a threshold or normalization to the similarity metric to enhance the accuracy of the match or to filter out weaker matches.
**6)Output Result**:<br>
The output of the template matching algorithm is often a map of similarity scores or the coordinates of the best match. This information can be used to identify the location of the template in the larger image
