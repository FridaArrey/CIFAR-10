## **1\. Introduction**

This project explores the process of building an image classification model for the CIFAR-10 dataset, which consists of 60,000 low-resolution images across 10 classes (e.g., cars, dogs, automobiles). This report documents our methodology, key findings, and final model performance.

## **2\. Trial 1: ResNet50 (Transfer Learning)**

Our initial approach involved using ResNet50, a powerful pre-trained model, with the expectation that its learned features would transfer to the CIFAR-10 dataset.

* **Result:** The model performed no better than random chance, achieving a final test accuracy of .  
* **Conclusion:** Transfer learning from a high-resolution dataset (like ImageNet, on which ResNet50 was trained) was not effective for the low-resolution CIFAR-10 images. This highlighted the importance of selecting an appropriate model architecture for the specific data.

## **3\. Trial 2: Simple CNN (Model from Scratch)**

Following the ResNet50 failure, we built a Simple Convolutional Neural Network from scratch to learn features directly from the CIFAR-10 data.

* **Result:** The model trained successfully, with both training and validation accuracy steadily increasing. It achieved a final validation accuracy of approximately 63%.  
* **Key Findings:** The model performed well on classes like automobiles and ships, with high F1-scores. It struggled with fine-grained classification problems, particularly with similar-looking classes such as cats, dogs, and birds, where F1-scores were significantly lower.

## **4\. Trial 3: Deeper CNN (Optimization)**

To further improve performance, we built a Deeper CNN with more layers. This model demonstrated successful learning but also exhibited signs of overfitting.

### **Overfitting Analysis**

After about Epoch 10, the model's training accuracy continued to increase, while its validation accuracy plateaued and began to fluctuate. This divergence indicates that the model was memorizing the training data and losing its ability to generalize.

### **Early Stopping: The Optimal Epoch**

To combat overfitting, we implemented an early stopping strategy by identifying the point of optimal performance. While the model achieved its peak validation accuracy at Epoch 17, a closer look at the metrics reveals a better choice.

* **13 Epochs (Optimal):** The training accuracy is 80.5% and validation accuracy is 79.6%. The small difference of just 0.9% indicates the model is generalizing well to new data and has not started to overfit. This is the ideal point to stop training.  
* **17 Epochs (Overfitting):** The training accuracy rises to 82.8%, but the validation accuracy actually drops back down to 79.6%. The difference between the two accuracies jumps to 3.2%. This confirms that overfitting is occurring, as the model's performance on the validation data has begun to degrade even as its performance on the training data continues to improve.

Epoch 13 shows the best balance: the point when validation accuracy plateaus or starts declining while training accuracy keeps improving.

## **5\. Conclusion and Final Model**

Our final model, the Deeper CNN trained for a precise duration of 13 epochs, represents our best-performing model. The project demonstrates the importance of not only choosing the right architecture but also using techniques like early stopping to prevent overfitting and achieve optimal, generalizable results.

