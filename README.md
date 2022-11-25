# Plants images classification
### Artificial Neural Networks and Deep Learning competition - Politecnico di Milano a.y. 2022/2023.
<p align="center">
Paolo Marzolo - Mark Federico Zampedroni - Marco Zanoni
</p>

## 1. Data  
The provided dataset contains 3542 labeled images (size 96x96) of plants for a total of 8 classes.

<p align="center">
<img src="/images/plants.PNG" alt="TF comparison">
</p>

Observations:
- The classes distribution is imbalanced.
- Species1 and Species6 consist only of 5.25% and 6.27% of the samples.
- Species1 and Species8 follow VERY similar patterns.

Our solutions:
- Stratified sampling.
- Data augmentation.
- Added class weights to the loss function.

## 2. Model

We used the most common design in image analysis: a Convolutional Neural Network.
Our main focus was on the model capability to distinguish Species1 and Species8, since it heavily effected the overall metrics and the other classes easily reached high accuracy.

### 2.1. Features  Extractor

The models available on Keras, if pre-trained on the ImageNet dataset, may have already learnt useful patterns to categorize images of plants or crops. 
Hence, we can download such models, keep only the feature extractor part and connect a simple classifier to evaluate their performance.

<p align="center">
<img src="/images/large3.PNG" alt="TF comparison">
</p>

ConvNeXtLarge outperforms the others. Its bottom has 295 layers and when the classifier is trained it reaches 87.27% accuracy.

### 2.2. Classifier

Using a dedicated validation set we tested various combinations of layers and reached the final result presented here.

<p align="center">
<img width="580px" src="/images/structure_with_input.PNG" alt="TF comparison">
</p>

Then we fine-tuned the whole network, including all but 90 of the layers in the convolutional part.

## 3. Test
Since the sets were created by doing stratified sampling the test results reflect the imbalanced distribution of classes samples.

- Accuracy : 94.67%
- Precision : 94.78%
- Recall : 93.17%
- F1 : 93.76%

![image](/images/confusion.PNG)

## 4. Competition evaluation
- First phase accuracy (30% test data): 93.25%
- Second phase accuracy (70% test data): 93.13%
