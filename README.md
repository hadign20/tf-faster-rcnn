# Description
This fork is to use the original tf-faster-rcnn for a task of multi-class vehicle detection in aerial images. The original faster R-CNN is used for Pascal-VOC data, and this is a customization suited for [VEDAI data](https://downloads.greyc.fr/vedai/) and also tested on [NWPU data](http://www.escience.cn/people/JunweiHan/NWPUVHR10dataset.html). It also provides an option to display Precision-Recall curve, after the testing is done.

# tf-faster-rcnn
A Tensorflow implementation of faster RCNN detection framework by Xinlei Chen (xinleic@cs.cmu.edu). This repository is based on the python Caffe implementation of faster RCNN available [here](https://github.com/rbgirshick/py-faster-rcnn).

**Note**: Several minor modifications are made when reimplementing the framework, which give potential improvements. For details about the modifications and ablative analysis, please refer to the technical report [An Implementation of Faster RCNN with Study for Region Sampling](https://arxiv.org/pdf/1702.02138.pdf). If you are seeking to reproduce the results in the original paper, please use the [official code](https://github.com/ShaoqingRen/faster_rcnn) or maybe the [semi-official code](https://github.com/rbgirshick/py-faster-rcnn). For details about the faster RCNN architecture please refer to the paper [Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](http://arxiv.org/pdf/1506.01497.pdf).


### Here are some sample results of performing this model on two datasets:

![](https://github.com/hadi-ghnd/tf-faster-rcnn/blob/master/data/imgs/figure_4.png)      |  ![](https://github.com/hadi-ghnd/tf-faster-rcnn/blob/master/data/imgs/figure_2.png)
:-------------------------:|:-------------------------:
Detection results in VEDAI |  Precision-Recal curve of each class


![]( https://github.com/hadi-ghnd/tf-faster-rcnn/blob/master/data/imgs/figure_21.png )      |  ![]( https://github.com/hadi-ghnd/tf-faster-rcnn/blob/master/data/imgs/figure_34.png )
:-------------------------:|:-------------------------:
Detection results in NWPU | Detection results in NWPU



# Object-Detection-from-Limited-Labelled-Data-
Innovative Deep Learning Object Detection Approach from Limited Labelled Data that Effectively Addresses Undetected False Negatives


### Introduction
The scientific basis of deep learning requires that a very large number of labelled training samples (infinite in theory) must be available in order for deep learning methods to achieve good performance. Specifically, according to the statistical learning theory [1], the upper bound of the actual risk is defined by two terms: the empirical risk and the confidence interval. While the empirical risk is a function of the training samples, the confidence interval specifies the capacity of the learning machine that is often quantified by the VC dimension. Only when the number of training samples approaches infinity, will the empirical risk approximate the actual risk. Otherwise, the confidence interval term is no longer negligible, and the empirical risk minimization based deep learning methods will not achieve the optimal performance. This is why deep learning methods always require a large number of labelled training samples for training the neural network systems. 
Labelling a large number of overhead satellite images, however, is either prohibitively expensive or simply unrealistic. Figure 1 shows an example overhead satellite image from the xView dataset, which indicates that the overhead satellite images often cover very large areas with an enormous number of objects, including many challenging targets like limited pixels or definition, high variability or mobility. A partial annotation will not work either for a deep learning method, as the unlabeled objects become the background or negative training samples, and as a result these objects will not be detected. 

![image](https://user-images.githubusercontent.com/24352869/188244982-d607d69d-3c68-48de-b80f-2f82de57cd46.png)

Current deep learning object detectors and the iterative bootstrapping method, albeit yielding some promising results, still lack robustness and suffer from limited labelled data. Their inherent drawbacks of introducing the undetected false negatives (UFNs) as negative training examples will lead to the ultimate failure in detecting those objects. The significance of meeting the above-mentioned difficult challenges by introducing an innovative approach is to “make the impossible possible”: for a large overhead satellite image dataset, it is impossible (prohibitively expensive) to exhaustively label all the instances of objects, but it is possible to selectively label a few instances for each object.

Towards that end, we propose an innovative Deep Learning (iDL) object detection approach from limited labelled data that effectively addresses undetected false negatives or UFNs with the following scientific benefits:

- An innovative Deep Learning (iDL) object detection approach that works from limited labelled data and integrates active learning and semi-supervised learning. The iDL approach improves upon the current deep learning methods because it works from limited labelled data. In contrast, the other deep learning methods require that the training data be completely labelled before learning occurs. Specifically, the proposed iDL method starts with carefully selecting a few representative training samples for each object, without exhaustively labelling all the instances. The remaining instances will be automatically detected in the following steps: the iDL approach that integrates active learning and the iDL approach that integrates semi-supervised learning. Note that during the iDL training, the unlabeled instances of objects will be excluded from the background or negative training examples using the following UFNs exclusion method. 

- A novel undetected false negatives (UFNs) exclusion method in iDL that excludes object instances from the background or the negative training examples for deep learning. We propose a novel method to effectively exclude the UFNs from the background or the negative training examples. Specifically, we will learn from the labelled data the threshold values for objects based on their statistical and color features, such as the SIFT, HOG, edges, and other local features. The regions, such as the UFNs, whose statistical values are larger than the threshold values, will be excluded from the background or the negative training examples. Note that this proposed idea also applies to the initial step of the iDL approach to exclude the unlabeled instances of objects from the background class by learning the threshold values for objects from the initial selectively labelled instances. 

- The iDL approach that integrates active learning. After the initial data samples are labeled, they are used as input to train a convolutional neural network or CNN, such as the representative object detection method, the scaled-YOLOv4 [32]. The trained model is tested against the unlabeled data to calculate the prediction scores, which are in turn used by the entropy-based sampling strategy to select the most informative batch. The most informative data samples are presented to the human reviewer for label confirmation or correction. 

- The iDL approach that integrates semi-supervised learning (SSL). For SSL, we apply the state-of-the-art Self-Training and the Augmentation driven Consistency regularization (STAC) method for automatic data labelling. In particular, the trained YOLOv4 model in the active learning process will be applied to generate pseudo-labels for the unlabeled data, which is augmented using color, geometric, and box-level transformations. The supervised and unsupervised losses are used in training the object detection model for loss minimization.

The objectives are multifaceted as listed below:
1.	An innovative Deep Learning (iDL) object detection approach will be developed that works from limited labelled data and integrates active learning and semi-supervised learning. The iDL approach starts with minimum labelling of a few representative samples for each object, without a complete labelling of a whole satellite overhead image, which covers a large area with an enormous number of object instances and takes tremendous amount of effort to label completely. 
2.	A novel undetected false negatives (UFNs) exclusion method will be developed to exclude unlabelled or missed object instances from the background or the negative training examples for the iDL approach. As a result, the small initially labelled data (incomplete labelling of the satellite overhead images) can now be applied for iDL training. In contrast, other deep learning methods will not work well on the incompletely labelled images. 
3.	The iDL approach that integrates active learning will also be developed, which requires only minimal human intervention for labelling more unlabeled data. 
	To avoid inefficient use of labeler’s time spent on confirming correct but uninformative detections, a novel entropy-based sample selection method will be developed to help choose more balanced samples from different object classes. Scientific basis: let us compare with the design of a support vector machine (SVM) – the vast majority of the training samples (e.g., more than 95%) are the uninformative non-support vectors, which do not contribute to the design of the SVM, whose maximal margin hyperplane is defined only by the support vectors. Following the same line of reasoning, the iDL approach capitalizes on the small number of representative training samples (like support vectors in SVM) per object for designing a more robust bootstrapping process. 
	A controlling number (R in Figure 4) will be defined to specify the portion of the data labeled in the active learning module with human intervention. This user-defined number (0 < R <= 1) controls automation vs. human intervention: if R = 1, all the data needs to be labeled reliably in the active learning module without considering the semi-supervised learning module. However, for minimal human intervention and maximal automation, we should have a smaller portion of the data to be labeled with human intervention and the remaining data to be labeled automatically in the semi-supervised module. Thus R provides a means for striking a balance between human intervention and automation.
4.	The iDL approach that integrates semi-supervised learning will be finally developed for fully automatic labelling of the remaining unlabeled data. Specifically, we will apply the state-of-the-art Self-Training and the Augmentation driven Consistency regularization (STAC) method for automatic data labelling. And with the additional labeled data, the bootstrapping process will further improve its object detection performance 
To summarize, our proposed research and development effort will produce an innovative deep learning approach that overcomes the difficult challenges from the current deep learning object detectors and the iterative bootstrapping method, provides strong scientific basis with the maximum amount of automation, and enables success for a more broadly-scoped Phase II R&D effort. 

### Active Learning
An innovative Deep Learning (iDL) object detection approach from limited labelled data that effectively addresses undetected false negatives is proposed. The iDL approach, which capitalizes on four innovative ideas, improves upon the current deep learning object detectors with the bootstrapping method. Specifically, first, the iDL approach works from limited labelled data, such as the initially selected a few representative training samples per object. In contrast, other deep learning methods do not work well on such incompletely labelled data. Second, the iDL approach presents a novel undetected false negatives (UFNs) exclusion method that excludes the unlabelled or missed object instances from the background or the negative training examples. Third, the iDL approach integrates active learning with minimal human intervention for labelling more unlabeled data. Fourth, the iDL approach integrates semi-supervised learning for fully automatic labelling of the remaining unlabeled data. Figure 2 shows the system architecture of the proposed iDL approach with the four innovative ideas discussed above. Note that the image classification module contributes to the first idea by balancing the choice of the initial pool of training samples.

![image](https://user-images.githubusercontent.com/24352869/188245109-d5714b5f-6c46-4dc8-9957-3b9dbfa8bcf6.png)


The novelty of the proposed iDL approach rests on the limited labelled data: the iDL approach works on a small set of partially labelled images while other deep learning methods require that all the instances of the objects be labelled in the images. Note that for the satellite overhead imagery, it is extremely challenging if not impossible to completely label all the instances in an image due to the huge geographic area covered by and the enormous number of objects in the image. 
To address the poor choice of the initial pool for the training data, we apply a deep learning method for image classification to balance the choice of the initial training images for each scene category as shown in Figure 3. Specifically, a convolutional neural network is trained with a number of image classification datasets, such as the UC Merced Land Use Classification Dataset. To avoid overfitting or underfitting, the capacity of the network should be chosen appropriately: high capacity often leads to overfitting and low capacity to underfitting. We will use the ResNet 50 deep learning model to be trained as an image classifier against a combination of publicly available satellite/aerial image classification datasets. The purpose of applying image classification is to obtain a fair number of images from each scene category in order to reduce the bias in the initial pool selection and keep the balance in the number of samples within each object category. 

Figure 3 shows the process of selecting an unbiased initial pool for labeling by means of image classification. The trained image classification model will categorize the images and the human reviewer will carefully select a number of images from each image category to construct an initial pool of representative samples with a predefined size (B in Figure 3). The goal in the selection process is to have a fair number of objects in each object class. 
The objects in the selected images will be manually labeled by a human annotator and these labelled samples are used as the input data to train our proposed iDL approach. Note that other deep learning methods do not work well on this initial training pool, because not all the object instances are labelled in the images. The iDL approach works by applying a novel undetected false negatives (UFNs) exclusion method that excludes the unlabelled or missed object instances from the background or the negative training examples. After the UFNs exclusion, the iDL approach will apply the state-of-the-art deep learning methods, such as the scaled-YOLOv4, the YOLTv4, and the SeMo-YOLO. The YOLTv4 and the SeMo-YOLO deep learning methods, for example, are developed for object detection in satellite imagery. These YOLO-based deep learning methods are presently the most efficient and demonstrating the state-of-the-art performance for the tasks such as object detection.

![image](https://user-images.githubusercontent.com/24352869/188245149-74150488-a78c-47f1-8b82-a56c14734702.png)


###  Undetected False Negatives (UFNs) Exclusion
iDL approach presents a novel undetected false negatives (UFNs) exclusion method that excludes the unlabelled or missed object instances from the background or the negative training examples. Specifically, we will apply a statistical learning approach that operates in parallel to the deep learning model in order to improve the detection results and correct the potential false detections. This module automatically learns various features, such as the HOG, SIFT, color, gradient, edges, and texture, from the reliably labeled samples. The learned features are used to establish thresholds for each region indicating the potential of that region to contain an instance of an object. If a region has the potential to contain an object, it will be removed from the background class in the training process of the deep learning model. Furthermore, the statistically learned thresholds may also be utilized at each round of the active learning to acquire the reviewer to confirm candidate locations where the deep convolutional neural network model might have missed an object. 
The iDL Approach that Integrates Active Learning 
The iDL approach further integrates active learning to label more unlabeled data with minimal human intervention. Actually, the iDL approach starts with the model trained using the initial pool of representative training samples for each object, and then applies active learning to further increase the number of training samples. Figure 4 shows the steps taken in the active learning module. Specifically, first, the initially trained model is tested against the unlabeled data pool to   
Figure 4) The architecture of the iDL approach that integrates active learning
calculate the prediction scores, which are in turn used by the entropy-based sampling strategy to select the most informative batch of images. The most informative data samples are presented to the human reviewer for object-level label confirmation or correction. Then the labeled samples are removed from the unlabeled pool and added to the labeled data pool. The scaled-YOLOv4 model is retrained with the updated pool of labeled data and tested against the updated unlabeled pool. 
Comparing with the simple bootstrapping procedure, our proposed process of presenting the chosen samples to the human labeler at each round is more efficient. The selected images contain the most informative images by estimating the image-level uncertainty values. In addition, the instance-level uncertainties are also derived, and the annotator will have an option to only confirm the instances with less than a specified level of certainty [5]. This technique can be implemented in the annotation GUI by indicating the most uncertain instances for confirmation or correction. As a result, our proposed approach can avoid the “inefficient use of labeler time spent confirming correct but uninformative detections”.
This procedure of the iDL active learning shown in Figure 4 will repeat until it reaches a user-defined number (R in Figure 4) that indicates the portion of the data should be labeled in the iDL active learning module with human intervention. This predefined number (0 < R <= 1) can be set to 1 in case we want all the data points to be labeled reliably in the active learning module without using the iDL semi-supervised learning. However, for minimal human intervention and maximal automation, we should have a smaller portion of the data to be labeled with the assistance of a human reviewer and the remaining data to be labeled automatically in the iDL semi-supervised learning module.
The labeled data obtained during the active learning process is a balanced set of samples in terms of including a fair number of object instances from different classes, which in turn improves the performance of our proposed iDL approach. In addition, since the balanced dataset contains a considerable number of samples from each object, the false negatives caused by lack of sufficient data for specific object classes will be significantly reduced.

![image](https://user-images.githubusercontent.com/24352869/188245188-8c630a07-7199-41ba-961e-5f257d16b214.png)


### Integration of Semi-supervised Learning 
The iDL approach integrates semi-supervised learning for fully automatic labelling of the remaining unlabeled data without human intervention. Figure 5 shows the details of the iDL approach with semi-supervised learning. In particular, the iDL approach with semi-supervised learning further labels the remaining portion of the unlabeled pool with the goal of reducing the manual work for further automation of the process. The portion of the data labeled by the iDL semi-supervised learning is set manually by the user: the user decides what percentage of the data is going to be labeled without a human in the loop. If set to 1, the entire data will be labeled in the active learning process to ensure the reliability of the generated labels. Otherwise, in the case of limited manpower, up to a large percentage of the data can be automatically labeled by the iDL semi-supervised learning module.
The Self-Training and the Augmentation driven Consistency regularization (STAC) method will be used. The trained YOLOv4 model obtained during the active learning process will be applied to generate pseudo-labels when tested against the unlabeled data. The unlabeled data will be augmented using color, geometric, and box-level transformations. The supervised and unsupervised losses will be used in the training of the object detection model with the purpose of minimizing the two losses. Figure 5 shows the detail steps of the iDL semi-supervised learning, which is designed based on the STAC method. Applying various data augmentation techniques results in fewer false negative detection caused by objects located at irregular places with different surroundings.
In order to suppress the number of undetected false negatives (UFNs), the confidence thresholds used in the filtering process of generating pseudo-labels are going to be chosen according to the sensitivity of each category of objects. The adaptive thresholds are assigned according to the number of instances in each object category, that is, to specify a larger threshold to the abundant categories, and a lower threshold to the scarce categories. This in turn, prevents the true positive samples from the rare object categories to be missed and therefore, reduces the number of undetected false negatives.
In addition, the proposed iDL approach is capable of expanding on the existing labelled datasets and adapting to new unseen object classes through continual learning. 

![image](https://user-images.githubusercontent.com/24352869/188245237-46b6556f-be3f-42d5-8047-b9d41d51c764.png)



![24](https://user-images.githubusercontent.com/24352869/188245629-7e63f7c9-0146-410d-8016-0c09040ce4d2.png)
![107](https://user-images.githubusercontent.com/24352869/188245630-6fc197fe-67f3-4572-80b2-9e59eb61bf03.png)
![825](https://user-images.githubusercontent.com/24352869/188245631-0b821a8a-fa21-4ec5-8e79-32e5c0e15217.png)
![1169](https://user-images.githubusercontent.com/24352869/188245632-acf47564-e0be-43a9-aadb-1e2a8ec856b3.png)
![1460](https://user-images.githubusercontent.com/24352869/188245635-a894b357-e77f-40df-ac8b-bbd1fe9ac7fc.png)
![1465](https://user-images.githubusercontent.com/24352869/188245636-bb5c24ab-0db4-471b-a03c-104bdb0ff579.png)
![2148](https://user-images.githubusercontent.com/24352869/188245637-959351cb-9262-4457-b6e5-b31cd88ddda2.png)
![2560](https://user-images.githubusercontent.com/24352869/188245831-48e7e191-5dc7-48d8-908f-f4fb0c6a9353.png)
![2571](https://user-images.githubusercontent.com/24352869/188245832-4866b8f1-de08-4d12-9a87-25b5b29e60a1.png)
![2621](https://user-images.githubusercontent.com/24352869/188245833-98940bf9-d645-4c9e-8425-da0fb2b1f7b8.png)
![7](https://user-images.githubusercontent.com/24352869/188245821-f977cdd6-7a03-4fcf-a4a9-3f5d5caa8513.png)
![92](https://user-images.githubusercontent.com/24352869/188245822-79132d09-15e1-4dd0-985d-c17a6c2a90fe.png)
![378](https://user-images.githubusercontent.com/24352869/188245823-cbc6890f-b069-4497-a88b-f5099049e466.png)
![511](https://user-images.githubusercontent.com/24352869/188245826-cc062b75-39bd-4a80-b791-dfafe8ddc8fc.png)
![1138](https://user-images.githubusercontent.com/24352869/188245828-7ef9b32a-566c-45ec-a44c-4da14d9b6c8f.png)
![1928](https://user-images.githubusercontent.com/24352869/188245829-ce99ee68-3249-4daa-9223-2b4099a971e2.png)
![2281](https://user-images.githubusercontent.com/24352869/188245830-229c296b-72fa-4738-8103-736b57419898.png)
