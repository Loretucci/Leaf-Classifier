# Leaf Classifier

## Project Overview
This project implements a Computer Vision pipeline to classify plant leaves as **Healthy** or **Damaged** (diseased). The goal is to automate the detection of leaf anomalies without relying on traditional supervised learning (like CNNs), but rather using image processing techniques to analyze color and structural properties.

The system compares three different approaches to identify the most robust method for agricultural image analysis.

## Technologies Used
* **Python 3.x**
* **OpenCV (`cv2`)**: For image processing, segmentation, and contour analysis.
* **Matplotlib**: For data visualization and result inspection.
* **NumPy**: For numerical operations.

## Methodology
The project explores three distinct methods for damage detection:

### 1. HSV Color Masking
* **Concept:** Isolates specific colors associated with disease (yellow/brown spots) using the HSV color space.
* **Process:**
    * Image Segmentation to remove the background.
    * Application of color masks to detect damaged areas.
* **Result:** Effective for high-contrast diseases but prone to false negatives when damage color blends with the leaf or background.

### 2. Contour Detection (Otsu's Thresholding)
* **Concept:** Uses structural analysis to find irregularities on the leaf surface.
* **Process:**
    * Conversion to grayscale and application of **Otsu's Binarization** to separate damage spots.
    * **Morphological Operations** to clean noise.
    * **Contour Analysis** (`cv2.contourArea`) to count and measure potential lesions.
* **Result:** Significantly higher accuracy than color masking. It effectively detects damage based on shape and contrast rather than just color.

### 3. Hybrid Approach (Cascade)
* **Concept:** A refinement strategy where images classified as "Healthy" by the Color Masking method are re-evaluated using Contour Detection.
* **Result:** Attempted to reduce false negatives, though the Contour Detection method alone proved to be the dominant factor in performance.

## Results & Conclusion
* **Color Masking:** Showed limitations in distinguishing subtle damage from background noise.
* **Contour Detection:** Emerged as the most reliable method, successfully identifying damage shapes that were missed by color analysis alone.
* **Key Takeaway:** Structural analysis (shape/contrast) proved more robust than chromatic analysis for this specific dataset.

## How to Run
1.  Clone the repository:
    ```bash
    git clone [https://github.com/YOUR_USERNAME/Leaf-Classifier.git](https://github.com/Loretucci/Leaf-Classifier.git)
    ```
2.  Install dependencies:
    ```bash
    pip install opencv-python matplotlib numpy
    ```
3.  Run the analysis notebook `analysis.ipynb` to see the pipeline in action.

## Project Structure
* `analysis.ipynb`: Main Jupyter Notebook containing the code and experiments.
* `final_main.py`: Helper functions for segmentation and detection logic.
* `original/`: Source dataset of leaf images.
* `segmented/`: Output of the segmentation step.
* `detected_*`: Output folders for classified images.

---
*Project developed for the Image Processing and Computer Vision course in collaboration with Hanif F. Hidayat (haniffurqon.hidayat@studio.unibo.it).*
