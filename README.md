```markdown
# Urbanization and Environmental Change Detection using EuroSAT and Google Earth Engine

This project demonstrates a methodology for detecting urbanization and other environmental changes between 2018 (EuroSAT dataset) and 2024 (Google Earth Engine Sentinel-2 imagery). It leverages a deep learning model trained on the EuroSAT dataset for land cover classification and then applies this model to recent satellite images to identify significant changes over time.

## Project Overview

The primary goal is to identify areas that have undergone land cover change, specifically focusing on potential urbanization and other environmental transformations. We start by training a Convolutional Neural Network (CNN) on the EuroSAT dataset, which consists of labeled Sentinel-2 satellite images. This trained model is then used to classify recent Sentinel-2 imagery (from 2024) for selected locations. By comparing the classifications, we pinpoint regions that have likely experienced changes.

## Key Components & Methodology

1.  **EuroSAT Dataset Processing**: The EuroSAT dataset, containing 13-band Sentinel-2 images categorized into 10 land cover classes, is used.
    *   Coordinates for each EuroSAT image are extracted to facilitate geographic comparison.

2.  **Deep Learning Model Training**: A TensorFlow/Keras CNN model is trained on the EuroSAT dataset to accurately classify land cover types. The model incorporates data augmentation, learning rate scheduling, and early stopping for robust performance.

3.  **Target Area Selection for 2024 Analysis**: To focus on relevant changes, a subset of 'natural' EuroSAT categories (e.g., Forest, River, Crop) from 2018 is sampled. For this project, 500 such points were randomly selected for further study.

4.  **2024 Satellite Image Acquisition (Google Earth Engine)**: For each of the sampled locations, a recent (2024) 13-band Sentinel-2 image patch is downloaded using the Google Earth Engine (GEE) API. The clearest, cloud-free image for each location in 2024 is prioritized.

5.  **Change Detection & Classification**: The trained CNN model classifies the 2024 image patches. The 2024 classification is then compared against the original 2018 EuroSAT label:
    *   **URBANIZATION**: If a 2018 'natural' class is classified as 'Residential', 'Industrial', or 'Highway' in 2024.
    *   **ENVIRONMENTAL CHANGE**: If the 2018 class differs from the 2024 class, but not categorized as 'URBANIZATION'.
    *   **STABLE**: If the 2018 and 2024 classifications match.

6.  **Confidence-Based Analysis**: The model's prediction confidence is used to identify the most certain changes, allowing for focused investigation of high-confidence transformations.

7.  **Urban Signature Verification**: An additional step is implemented to identify more 'definite' urban changes by analyzing the spectral signature of the 2024 patches (e.g., high brightness and 'grey' characteristics in RGB bands, typical of concrete/buildings).

8.  **Visualization**: Results are visualized using:
    *   `matplotlib` to display individual image patches (2018 vs. 2024).
    *   `folium` to generate interactive geographical maps highlighting different types of changes.

## Results & Findings

The project successfully identifies and categorizes land cover changes. A key outcome is the identification of locations showing strong indicators of urbanization, which are further verified using spectral analysis. An interactive map (`FINAL_URBAN_REPORT_MAP.html`) is generated, distinguishing between general environmental changes and verified urban developments.
You can acces the deployed application:https://siyaram322.github.io/EUROSAT-ENVIRONMENTAL--CHANGE-URBANIZATION--DETECTION/
## Technologies Used

*   **Python**
*   **TensorFlow/Keras**: For building and training the CNN model.
*   **Rasterio**: For reading and processing GeoTIFF satellite imagery.
*   **Google Earth Engine (GEE)**: For accessing and downloading up-to-date Sentinel-2 imagery.
*   **Pandas**: For data manipulation and analysis.
*   **Scikit-learn**: For data splitting and label encoding.
*   **Matplotlib & Seaborn**: For static data visualization.
*   **Folium**: For interactive geographical mapping of change points.
*   **OpenCV (cv2)**: For image preprocessing tasks like resizing.

## How to Reproduce

1.  **Clone the Repository**.
2.  **Set up Google Earth Engine**: Ensure you have a Google Cloud project set up and have authenticated GEE in your environment. Instructions for `ee.Authenticate()` and `ee.Initialize()` are crucial.
3.  **Download EuroSAT Dataset**: Obtain the EuroSAT dataset (13-band version) and place it in the specified `root_dir` (e.g., `/content/drive/MyDrive/Eurosat/Eurosat/EuroSATallBands`).
4.  **Run the Jupyter Notebook** (or Colab notebook if provided). The notebook guides through all steps from data preparation to change detection and visualization.

Feel free to explore the code and adapt it for your specific change detection tasks!
```
