Why XAI?
XAI stands for eXplainable Artificial Intelligence. It refers to the method and techniques used to make AI systems more transparent, understandable, and interpretable to humans. XAI techniques are used to provide insights into the inner workings of AI models, helping researchers and developers understand why models make certain predictions or classifications.

The XAI technique used to explain classification of Resnet and Densenet models is GradCAM.

What is GradCAM?

Grad-CAM stands for Gradient-weighted Class Activation Mapping. This is a technique used in the field of ComputerVision to understand and visualize the decisions made by a CNN, particularly in image classification tasks. It helps in explaining which regions of an input image are important for CNN's prediction.

How it works?
Forward Pass: The input image is passed through the CNN, and the output of interest is identified. This could be the score corresponding to the predicted class.
Compute Gradients: The gradients of the target class score wrt the feature maps of the last convolution layer are computed. These gradients represent the importance of the final convolutional layer’s feature maps to the target class
Heatmap Generation: Finally a weighted combination of the last convolution layer’s feature maps is computed.This results in a heatmap that highlights the regions in the input image that contributed the most to the CNN’s decision for the target class.

The heatmap produced by Grad-CAM visually shows which parts of the input image were most influential in CNN's decision-making process. This visualization can help researchers and developers understand and interpret the decisions made by CNNs, providing insights into their inner workings and potentially aiding in debugging and improving model performance


Implementation perspective:

We use 2 functions - one is to make the gradients into heatmap, and another is to visualize the heatmap on top of the original image.

Make_gradcam_heatmap: 
This function takes in image array, model and the last convolution layer as inputs. 
It creates a sub-model that outputs both feature maps of the last convolution layer and the model predictions. 
Using GradientTape, it records the gradients of the predicted class score wrt the output of the last convolution layer. 
The gradients are then computed by multiple feature maps of the last convolution layer with the computed channel importance values
The heatmap is then normalized to a range of [0,1]
Display_gradcam:
It takes the original image and the generated heatmap as input.
Rescales the heatmap to the range [0,255]
It creates the heatmap using the help of colormap.
The heatmap is resized to the original image size.
Finally the heatmap is superimposed on the original image.
