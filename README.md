# Enhancing Semantic Image Understanding with Fine-Tuned CLIP
In this mini project, I fine-tuned the image encoder of CLIP (Contrastive Language-Image Pre-training) using pairs of images from the CIFAR-10 dataset. The goal was to enhance the model's ability to make images within the same class more similar while making images from different classes more dissimilar. To achieve this, I employed a custom loss function designed to encourage the model to learn meaningful representations of images based on their semantic content.

The custom loss function (Contrastive Loss) leverages cosine similarity between the embeddings of two images. By maximizing the cosine similarity for images within the same class and minimizing it for images from different classes, the model learns to effectively discriminate between different classes while capturing the underlying similarities within each class.

Let $S_{i,j}$ represent the cosine similarity between embedding vectors $\text{emb}_i$ and $\text{emb}_j$. 

The loss $L_{i,j}$ between embeddings $\text{emb}_i$ and $\text{emb}_j$ can be defined as:

$$
L_{i,j} = (1 - \text{label}) \times S_{i,j} + \text{label} \times (1 - S_{i,j})
$$

where $\text{label}$ is a binary indicator variable defined as follows:
- $\text{label} = 1$ if $\text{emb}_i$ and $\text{emb}_j$ belong to the same class,
- $\text{label} = 0$ otherwise.

This approach is particularly fascinating for image search and retrieval tasks. By embedding images into a shared semantic space, we enable efficient similarity-based retrieval. This means that given a query image, we can retrieve images with similar semantic content from a large dataset. This capability has numerous applications, from content-based image retrieval in digital libraries to visual search in e-commerce platforms. By fine-tuning CLIP in this manner, we not only enhance its performance on classification tasks but also empower it for various downstream applications requiring image understanding and retrieval.

# Results

![3](https://github.com/Abdennacer-Badaoui/CLIP_Finetuning/assets/106801897/ae181123-f7f4-466e-beed-68554def7fb1)
![4](https://github.com/Abdennacer-Badaoui/CLIP_Finetuning/assets/106801897/3b52895d-7677-4cc2-8864-ca9e8d288680)

Let's compare the similarities from the original and fine-tuned CLIP models based on the provided heatmaps:

### Original CLIP Model Similarities:
- The original CLIP model shows a range of similarities between different image pairs, with higher similarity scores for some pairs even if they don't belong to the same class.
- Notably, some dissimilar pairs (e.g., image pairs from different classes) still have relatively high similarity scores, indicating that the model doesn't perfectly distinguish between different classes.
- Examples of high similarities between different classes include:
  - The horse and the cat (0.6770).
  - The plane and the car (0.5328).

### Fine-tuned CLIP Model Similarities:
- After fine-tuning, the similarities for images from the same class are more distinct and higher, indicating the model has learned to better group images within the same class.
- Dissimilar pairs have significantly lower similarity scores, showing that the model has learned to better differentiate between images from different classes.
- Examples of clear improvements include:
  - The horse (index 0) and the horse (index 4) have a high similarity score (0.9232) after fine-tuning.
  - The cat (index 3) and the cat (index 7) also show improved similarity (0.8971).
  - The similarity between different classes, such as the horse (index 0) and the car (index 2), is reduced (0.1799).

# Analysis of Mean Similarity Matrices

Below is a summary of the comparison based on the provided mean similarity matrices.
![5](https://github.com/Abdennacer-Badaoui/CLIP_Finetuning/assets/106801897/23f2c05d-971a-435f-9404-e552ecccbaf3)
![6](https://github.com/Abdennacer-Badaoui/CLIP_Finetuning/assets/106801897/bcba3aef-d069-4810-961d-3ab697c1233f)

### Observations:

- Original CLIP Model:
  - The mean similarity scores are generally high (mostly above 0.8) across all classes.
  - There is a high degree of intra-class similarity (diagonal elements are close to 1.0).
  - Inter-class similarities are also relatively high, indicating that the original CLIP model does not distinctly separate different classes well.

- Fine-tuned CLIP Model:
  - The mean similarity scores are more varied, with many scores significantly lower than those of the original model.
  - Intra-class similarities remain high, but inter-class similarities are lower compared to the original model.
  - The fine-tuned model shows better separation between different classes (lower inter-class similarity scores), which indicates better discriminative power for the CIFAR-10 dataset.


### Summary:
Fine-tuning has made the CLIP model more effective at distinguishing between different classes and reinforcing the similarity within the same class. This is evident from the heatmaps where:
- Same-class pairs have higher similarity scores in the fine-tuned model compared to the original.
- Different-class pairs have lower similarity scores in the fine-tuned model, indicating better separation of distinct categories.

This fine-tuning process enhances CLIP's performance in tasks like image search and retrieval, where accurately grouping similar images and separating dissimilar ones is crucial. This improvement is visually represented in the heatmaps, demonstrating the effectiveness of the fine-tuning approach.
