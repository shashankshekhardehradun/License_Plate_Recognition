            AUTOMATIC LICENSE PLATE RECOGNITION

            ASADEL TECH


OBJECTIVE- 

1. Perform segmentation of characters
2. Train a ML model to predict characters
3. Prediction of characters in License Plate

INTRODUCTION-

The report demonstrates the work done and the results obtained for the license plate recognition project undertaken during December, 2018 for ASADEL TECH.

APPROACH-

1. CHARACTER SEGMENTATION

The approach used to segment the images is Connected Component Analysis. Connected regions will imply that all the connected pixels belong
to the same object. A pixel is said to be connected to another if they both have the same value and are adjacent to each other.

Car Image -> Grayscale Image -> Binary Image -> Applying CCA to get connected regions -> Detect license plate out of all connected regions
(Assumptions made : width of the license plate region to the full image ranges between 5% and 40% and height of the license plate region
to the full image is between 8% & 20%)

Otsu’s binarization is used to convert a grayscale image into a binary image. 
The following explains in detail the process of binarization which was integrl in segmenting the images.

OTSU’S BINARIZATION-

In image analysis, we often need an automatic, data-driven way to distinguish two types of relatively homogenous things, like land vs. water, forest vs. grass or foreground vs. background. For single-band images that have a bimodal pixel distribution, a two-class segmentation can be performed by finding a single threshold that separates the two classes.

Otsu’s method is a means of automatically finding an optimal threshold based on the observed distribution of pixel values (Otsu. 1979).

First, let’s define optimal as Otsu did: whatever partition of the data that maximizes inter-class variance (equivalently, minimizes the sum of intra-class variances). Define inter-class variance as BSS/p, where BSS (between-sum-of-squares) is







In our case, there are two classes so p=2. Here we’re using the between-sum-of-squares (BSS) terminology to indicate that this is a general method to describe the variance structure of a dataset.

We’re looking for that threshold that maximizes the BSS.
We’re not going to search exhaustively. We’re just going to search over the thresholds that are represented by the bins in a histogram. The advantage of that approach is that it only requires a single pass over the data. At each bin of the histogram, define class k as the pixels in that bin and lower. Class k+1 is everything else. 
The function looks at every possible partition of the input data defined by the bins of the histogram, then returns the mean associated with the bin that maximizes the BSS. This works better when you strategically choose the region for which the histogram is generated. A rudimentary mask is obtained by this with the two components being the sure foreground and the sure background region. 

The resulting mask is then inverted so that the characters are distinctly visible over the background.

Now, the output of the  binarization is used as input for Connected Component Analysis which is explained below.

CONNECTED COMPONENT ANALYSIS-

Connected components labeling scans an image and groups its pixels into components based on pixel connectivity, i.e. all pixels in a connected component share similar pixel intensity values and are in some way connected with each other. Once all groups have been determined, each pixel is labeled with a graylevel or a color (color labeling) according to the component it was assigned to. 
Extracting and labeling of various disjoint and connected components in an image is central to many automated image analysis applications. 
Connected component labeling works on binary or graylevel images and different measures of connectivity are possible. However, for the following we assume binary input images and 8-connectivity. The connected components labeling operator scans the image by moving along a row until it comes to a point p (where p denotes the pixel to be labeled at any stage in the scanning process) for which V={1}. When this is true, it examines the four neighbors of p which have already been encountered in the scan (i.e. the neighbors (i) to the left of p, (ii) above it, and (iii and iv) the two upper diagonal terms). Based on this information, the labeling of p occurs as follows: 
If all four neighbors are 0, assign a new label to p, else 
if only one neighbor has V={1}, assign its label to p, else 
if more than one of the neighbors have V={1}, assign one of the labels to p and make a note of the equivalences. 
After completing the scan, the equivalent label pairs are sorted into equivalence classes and a unique label is assigned to each class. As a final step, a second scan is made through the image, during which each label is replaced by the label assigned to its equivalence classes. For display, the labels might be different gray levels or colors. 

2. CHARACTER PREDICTION
Model is trained using SVC (4 cross fold validation) with dataset present in directory train 20X20. The model is saved as finalized_model.sav
which is then loaded to predict each character. SVC has been explained in brief below.

SUPPORT VECTOR CLASSIFIER-

“Support Vector Machine” (SVM) is a supervised machine learning algorithm which can be used for both classification or regression challenges. However, it is mostly used in classification problems. In this algorithm, we plot each data item as a point in n-dimensional space (where n is number of features you have) with the value of each feature being the value of a particular coordinate. Then, we perform classification by finding the hyper-plane that differentiate the two classes very well (look at the below snapshot).

















Support Vectors are simply the co-ordinates of individual observation. Support Vector Machine is a frontier which best segregates the two classes (hyper-plane/ line). It uses a subset of training points in the decision function (called support vectors), so it is also memory efficient. 

Once the characters of plate is obtained and model is trained, the model is loaded in order to predict each character.



