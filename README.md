# Amazon-ML-Challange-2024
Product Entity Extraction Using Zero-Shot Prompting


### Competition Host: Unstop
### Date: Oct’24


---

Ashish Kumar Uchadiya

- Team: TAMS
- contributers: Shivam Negi, Mayur Dhanawade, Tarun Bhist

![Alt text](https://github.com/akuresonite/Amazon-ML-Challange-2024/blob/main/Rank/amazon_ml_rank.jpg)



## Feature Extraction from Images

In this hackathon, the goal is to create a machine learning model that extracts entity values from images. This capability is crucial in fields like healthcare, e-commerce, and content moderation, where precise product information is vital. As digital marketplaces expand, many products lack detailed textual descriptions, making it essential to obtain key details directly from images. These images provide important information such as weight, volume, voltage, wattage, dimensions, and many more, which are critical for digital stores.

### Data Description: 

The dataset consists of the following columns: 

1. **index:** An unique identifier (ID) for the data sample
2. **image_link**: Public URL where the product image is available for download. Example link - https://m.media-amazon.com/images/I/71XfHPR36-L.jpg
    To download images use `download_images` function from `src/utils.py`. See sample code in `src/test.ipynb`.
3. **group_id**: Category code of the product
4. **entity_name:** Product entity name. For eg: “item_weight” 
5. **entity_value:** Product entity value. For eg: “34 gram” 
    Note: For test.csv, you will not see the column `entity_value` as it is the target variable.

### Output Format:

The output file should be a csv with 2 columns:

1. **index:** The unique identifier (ID) of the data sample. Note the index should match the test record index.
2. **prediction:** A string which should have the following format: “x unit” where x is a float number in standard formatting and unit is one of the allowed units (allowed units are mentioned in the Appendix). The two values should be concatenated and have a space between them. For eg: “2 gram”, “12.5 centimetre”, “2.56 ounce” are valid. Few invalid cases: “2 gms”, “60 ounce/1.7 kilogram”, “2.2e2 kilogram” etc.
    Note: Make sure to output a prediction for all indices. If no value is found in the image for any test sample, return empty string, i.e, `“”`. If you have less/more number of output samples in the output file as compared to test.csv, your output won’t be evaluated. 


### Constraints

1. You will be provided with a sample output file and a sanity checker file. Format your output to match the sample output file exactly and pass it through the sanity checker to ensure its validity. Note: If the file does not pass through the sanity checker, it will not be evaluated. You should recieve a message like `Parsing successfull for file: ...csv` if the output file is correctly formatted.

2. You are given the list of allowed units in constants.py and also in Appendix. Your outputs must be in these units. Predictions using any other units will be considered invalid during validation.

### Evaluation Criteria

Submissions will be evaluated based on F1 score, which are standard measures of prediction accuracy for classification and extraction problems.

Let GT = Ground truth value for a sample and OUT be output prediction from the model for a sample. Then we classify the predictions into one of the 4 classes with the following logic: 

1. *True Positives* - If OUT != `""` and GT != `""` and OUT == GT
2. *False Positives* - If OUT != `""` and GT != `""` and OUT != GT
3. *False Positives* - If OUT != `""` and GT == `""`
4. *False Negatives* - If OUT == `""` and GT != `""`
5. *True Negatives* - If OUT == `""` and GT == `""` 

Then, F1 score = 2*Precision*Recall/(Precision + Recall) where:

1. Precision = True Positives/(True Positives + False Positives)
2. Recall = True Positives/(True Positives + False Negatives)


### Appendix

```
entity_unit_map = {
  "width": {
    "centimetre",
    "foot",
    "millimetre",
    "metre",
    "inch",
    "yard"
  },
  "depth": {
    "centimetre",
    "foot",
    "millimetre",
    "metre",
    "inch",
    "yard"
  },
  "height": {
    "centimetre",
    "foot",
    "millimetre",
    "metre",
    "inch",
    "yard"
  },
  "item_weight": {
    "milligram",
    "kilogram",
    "microgram",
    "gram",
    "ounce",
    "ton",
    "pound"
  },
  "maximum_weight_recommendation": {
    "milligram",
    "kilogram",
    "microgram",
    "gram",
    "ounce",
    "ton",
    "pound"
  },
  "voltage": {
    "millivolt",
    "kilovolt",
    "volt"
  },
  "wattage": {
    "kilowatt",
    "watt"
  },
  "item_volume": {
    "cubic foot",
    "microlitre",
    "cup",
    "fluid ounce",
    "centilitre",
    "imperial gallon",
    "pint",
    "decilitre",
    "litre",
    "millilitre",
    "quart",
    "cubic inch",
    "gallon"
  }
}
```
