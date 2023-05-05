Download Link: https://assignmentchef.com/product/solved-cv1-assignment-2
<br>
<strong>Task 1: </strong>Template matching (programming)

Correlation filters respond most strongly to regions of images that look like the filter itself. This property is used for template matching. In template matching, we cross correlate a template with an image. The template is another image that is a prototype for what we want to localize in an image. The cross-correlation is the strongest where the image looks most like the template.

Download a clock template image and an image containing a clock from Moodle under the names coco264316clock.jpg and coco264316.jpg, respectively.

Read the template and the image. Convert them to grayscale.

Use the function skimage.feature.match_template to compute the normalized correlation between two images. Visualize the matching result. Verify that the brightest pixel in the result corresponds to the clock.

Flip the template horizontally. Verify that the clock can no longer be found.

<strong>Task 2: </strong>Edge detection (programming)

Noise negatively affects edge detection. To examine the effect of this in practice, we apply edge detection on a noisy image and a smoothed image.

Load the image woman.png provided. Note that it is already grayscale.

Using skimage.util.random noise, add Gaussian distributed noise to the image with a variance of 0.01. This gives you a noisy image <em>N</em>.

Apply skimage.filters.gaussian to filter <em>N</em>. Use <em>σ </em>= 1<em>.</em>0. This gives you a smoothed image <em>S</em>.

Next, apply the Sobel filter as follows.

Use the function skimage.filters.sobel. This function applies the two Sobel kernels (horizontal and vertical) on the image, and then computes the root of the squared sum of the results.

Visualize the result of applying the function on the noisy image <em>N</em>, and on the smoothed image <em>S</em>.

Suppose the output of the sobel function on the noisy image is <em>F<sub>n </sub></em>and the output on the smoothed image as <em>F<sub>s</sub></em>.

Select two threshold values <em>t<sub>n </sub></em>and <em>t<sub>s </sub></em>for edge detection. Draw histograms of intensity values in <em>F<sub>s </sub></em>and <em>F<sub>n </sub></em>to come up with suitable threshold values.

Create a binary mask by applying the logical operations <em>F<sub>n </sub>&gt; t<sub>n </sub></em>and <em>F<sub>s </sub>&gt; t<sub>s </sub></em>in NumPy. The parts of the image where the threshold is exceeded (there is an edge) are indicated by true values. Visualize the binary masks.

Tune your threshold values until the detected edges show the outline of the woman’s face.

Did you notice it is almost impossible to tune the threshold for the noisy image to show just the outline of the face? Why is edge detection improved by applying smoothing?

<strong>Task 3: </strong>Image pyramids (programming)

Recall the Gaussian image pyramid as shown in the image below.

Figure 1: A Gaussian image pyramid with four layers. Image by user “Cmglee”, Wikipedia.

In this task, we use Gaussian pyramids to calculate a saliency map, following the procedure illustrated in Figure 2. The approach generates two Gaussian pyramids, a center pyramid and a surround pyramid. Subtracting two layers from these pyramids corresponds to applying a Difference of Gaussian filter. This is useful to detect contrasts in images, which is the basis for saliency computation.

First read the documentation of the function skimage.transform.pyramids.pyramid gaussian online. Load the image visual attention.png from Moodle, and convert it to grayscale. Then, calculate the center and surround pyramids. Use the following parameters:

Use max layers=4 to obtain five layers as shown in Figure 1.

Center pyramid: <em>σ</em><sub>1 </sub>= 9,

Surround pyramid: <em>σ</em><sub>2 </sub>= 16.

We shall denote layer <em>j </em>of the center pyramid by <em>C<sub>j </sub></em>and layer <em>j </em>of the surround pyramid by <em>S<sub>j</sub></em>. Visualize each of the layers in both pyramids.

Next, calculate <em>on-off contrast pyramid </em>and the <em>off-on contrast pyramid </em>as follows:

Figure 2: Saliency computation using two difference-of-Gaussian pyramids

For the on-off contrast pyramid, the <em>j</em>th layer is given by <em>C<sub>j </sub></em>− <em>S<sub>j</sub></em>

For the off-on contrast pyramid, the <em>j</em>th layer is given by <em>S<sub>j </sub></em>− <em>C<sub>j</sub></em>

Important: use np.clip to clip values from both subtractions to the range [0<em>,</em>1].

Visualize each of the layers in both pyramids.

For both the on-off pyramid and the off-on pyramid, calculate the feature maps for both pyramids as follows:

Upsample each layer <em>j </em>≥ 2 to the same size as layer <em>j </em>= 1. Use skimage.transform.resize which will perform interpolation to upsample.

Average all layers pixelwise to obtain the feature map.

Visualize the average image.

Finally, calculate the conspicuity map or saliency map by averaging the two feature maps (on-off and off-on). Visualize the final conspicuity map.

What are the differences of this approach of computing a saliency map compared to the integral image method from assignment sheet 1? What are the advantages of the approach based on image pyramids?