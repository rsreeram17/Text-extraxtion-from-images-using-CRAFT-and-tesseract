# Text detection and extraction using CRAFT and Tesseract

## Approach

Since the objective used here is to extract textual information from the images, the entire process was divided into two parts:

1. Text detection
2. Text extraction

#### Text detection

The objective was to identify the bounding boxes for the parts of the images containing textual information. Based on research  Character-Region Awareness For Text detection (CRAFT) and Efficient accurate scene text detector (EAST) models were found to be the widely used text detection models. The model used here is CRAFT and due to time constrains, predictions by EAST model was not explored completely. However I did try using EAST model for detection.

There was no training done on the model and the all the results are by using the already trained model weights and default hyper parameters.

#### Text extraction

Once the bounding boxes were formed, the next step was to extract the textual information in those regions. Tesseract model was used for this exercise. (using python wrapper - pytesseract)

For each image, regions proposed by the CRAFT model was cropped and fed into the tesseract model to extract the text. 

## Model evaluation

#### Text detection

Intersection over union (IOU) was the chosen metric for the valuation of bounding box predictions. IOUs for the predicted bbox and ground truth bbox and based on the threshold, true positives, false positives and false negatives were calculated and using this average precision and recall were calculated. The logic used for the calculation can be found in the code notebook.

With a IOU threshold of 0.6 following are the average precision and recall:

Average precision: 0.88
Average recall: 0.91

####  Text extraction

For the text extraction evaluation, word error rate was the only metric used. For each of the true positive predictions, the word error rate between the text extracted by tesseract and the actual text in the bbox was calculated. Total error rate for the model was calculated as the number of word error rates upon total words.

WER for the model: 0.64

**Note:** Even if there is one character predicted wrongly, the predicted word is flagged as an error.

## Suggestions/Next steps

With the steps listed below we could possibly improve the performance for both text detection and text extraction (Very important because of high wer currently):

- Explore other open source text detection and text extraction models like EAST (text detection), Google OCR(text extraction) etc.

- Retrain the current models with additional images

- Use heuristic logics on the text extractions to make better final text outputs

  