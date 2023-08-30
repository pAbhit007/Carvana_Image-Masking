# Carvana_Image-Masking
It as a Carvana Image Masking challenge in which it challenged to develop an algorithm that automatically removes the photo studio background. This will allow Carvana to superimpose cars on a variety of backgrounds. You’ll be analyzing a dataset of photos, covering different vehicles with a wide variety of year, make, and model combinations.

Here's a detailed process of how image masking is typically performed in machine learning:

#### Data Collection and Preparation:

The dataset was large so we needed to divide it in batches of 4 to train it on model and also imported the required libraries for this. We used MyDataset class that inherits from torch.utils.data.Dataset. This class handles loading and preprocessing of the images and their corresponding masks for the segmentation task.
The dataset is split into training, validation, and test sets. 80% of the data is used for training, and the remaining data is split equally between validation and test sets.
Annotate the dataset by creating ground truth masks. These masks are binary images where pixels corresponding to the object of interest are marked as foreground (usually white) and pixels corresponding to the background are marked as background (usually black).

#### Choosing a Model:
Usual Convolutional Neural Networks (CNNs) models were not giving impressive results for this datasets and their accuracy were around 75 percent. So to improve the accuracy and further results, conventional TransUnet model was added with dilation layer to improve the results and the accuracy increased upto 98 percent.

#### Model Architecture:
It comprises various components, including convolutional layers, downsampling paths, upsampling paths, and an output layer for segmentation. The architecture follows a U-shaped design, combining both convolutional and transformer-based elements. It takes as input an image with n_channels channels and produces segmentation masks with n_classes classes. The model begins with a double-convolutional layer with dilation for context capture. It subsequently employs downsampling blocks to progressively reduce spatial dimensions and capture hierarchical features. Upsampling paths are used to recover spatial information and combine features from the downsampling path using skip connections. The final output is obtained through a convolutional layer followed by a sigmoid activation function to produce pixel-wise segmentation probabilities. The model's architecture, with its combination of convolutional and transformer-based components, makes it suitable for segmenting objects in images with a focus on capturing contextual information efficiently.

#### Training:
Train the model using the annotated dataset and the chosen architecture.
Traditional BCE Loss was not effective so hybrid Loss was used here to improve the performance metrics, that measure the difference between the predicted mask and the ground truth mask.
Monitored the training process and adjusted hyperparameters as needed.

#### Validation and Testing:
Evaluated the trained model on a validation dataset to ensure it's not overfitting and is generalizing well to new data.
Also Fine-tuned the model if necessary based on validation results.


#### Visualization and Analysis:
Overlayed the predicted mask on the original image to visualize the masked regions.
Various Perfomance Metrics such as Dice Score, Precision, IoU etc. were giving impressive results



### Qualitative Performance
<img width="616" alt="image" src="https://github.com/pAbhit007/Carvana_Image-Masking/assets/111629488/a7f935d3-6462-4db0-8608-8cff99d3d861">
