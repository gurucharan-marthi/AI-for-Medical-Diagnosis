# Week 3 Quiz: Segmentation on medical images

### Notice that I only list correct options.

1. Which of the following is a segmentation task?

- **Determining which areas of the brain have tumor from an MRI**

Correct! Classification tasks have binary or categorical labels for each image, while segmentation tasks ask you to determine a label for every pixel (or voxel).

2. What is the MAIN disadvantage of processing each MRI slice independently using a 2D segmentation model (as mentioned in the lecture)?
Hint: watch the lecture video "Segmentation" to help you answer this question.

- **You lose some context between slices**

Correct! The main disadvantage is the loss of information between slices. For example, if a tumor is present in a given slice, then we would expect higher probability of having a tumor in the same area in neighboring slices.

3. The U-net consists of...

- **A contracting path followed by an expanding path**

Correct! The U-net consists of a contracting path followed by an expanding path. This can be interpreted as ‘squeezing the input to create a low dimensional representation and then producing a segmentation based off of those low dimensional features.

4. Which of the following data augmentation is most effective for MRI sequences?

- **Rotation**

Correct! The only transformation which preserves the integrity of the data is using rotations. If we shuffle the slices, the relationships between the slices will change and the model will not be able to learn.

5. What is the soft dice loss for the example below?
L(P,G) = 1 - \frac{2\sum_{i=1}^n p_i g_i}{\sum_{i=1}^n p_i^2 + \sum_{i=1}^n g_i^2}

- **0.089**

Correct! Using the formula:
L(P,G) = 1 - \frac{2\sum_{i=1}^n p_i g_i}{\sum_{i=1}^n p_i^2 + \sum_{i=1}^n g_i^2}
Computing the numerator, we get 2 * ( 3.7) = 7.4, and the denominator is 3.13 + 5.0 = 8.13. Therefore the answer is 1 - (7.4 / 8.13) = 0.089.

6. Look at the output of model 1 and model 2: Which one will have a lower soft dice loss?
Hint: Notice the prediction scores of P1 and P2 on the pixels where the ground truth is 1. This may help you focus on certain parts of the soft dice loss formula:


- **Model 1 has a lower loss**

Correct! Note that the numerator will not change between the models, since the scores for model 1 and 2 are the same for the pixels which have ground truth 1.
However, the denominator for model 1 will be smaller, since it has smaller scores on the corner pixels (0.3 for model 1 instead of 0.5 for model 2).
With a smaller denominator, the ratio for model 1 will be larger. Subtracting 1 minus the larger ratio will lead to a smaller loss for model 1.

7. What is the minimum value of the soft dice loss?
L(P,G) = 1 - \frac{2\sum_{i=1}^n p_i g_i}{\sum_{i=1}^n p_i^2 + \sum_{i=1}^n g_i^2}

- **0**

Correct! The minimum value is 0. To see this, set p_i = g_i. Then the numerator will be equal to the denominator and 1 minus that will be 0.
To see that it is greater than or equal to 0, note that the top will be bounded above by both \sum_{i=1}^n p_i^2 and \sum_{i=1}^n g_i^2
Therefore, 2 times the numerator is less than or equal to the denominator, so this fraction must be at most 1. So the loss must be greater than or equal to 0.

8. An X-ray classification model is developed on data from US hospitals and is later tested on an external dataset from Latin America. Which if the following do you expect?

- **Performance drops on the new dataset**

Correct! We would expect performance to drop on the new external dataset since the underlying population of the new patient population is different from the population the model was trained on. Additionally, there might be idiosyncrasies about the scanners for the X-rays on the new dataset that bias the model. We would not typically expect performance to remain constant or improve, just like we don’t expect the model performance on the test set to be the same as on the validation set after hyper-parameter tuning.

9. Which of the following is an example of a prospective study?

- **A model is deployed for 1 year in an emergency room and its performance over that time is evaluated**

Correct! A prospective study is the application of a model to data that is not historical.
