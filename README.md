# NOVOUS

<p align="center">
  <a>
    <img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/logo.png" alt="Logo" width="180" height="140">
  </a>
  <h3 align="center">EatBetterNotLess</h3>
  <p align="center">
    The app that assesses the quality of packaged food products and recommends healthier substitution.
    <br />
    <a href="https://docs.google.com/presentation/d/18U59q65M4gWwAdbxB0iUPPr1RTWVEJv36mlMCbqDrYg/edit?usp=sharing"><strong>The Presentation »</strong></a>
    <br />
    <br />
    <a href="https://github.com/thuminhle59/Novous_EatBetterNotLess/tree/main/Project_Files">Jupyter Notebooks</a>
    ·
    <a href="https://world.openfoodfacts.org/data">Dataset</a>
  </p>
</p>

## DATASET
The dataset used for Novous originates from OpenFoodFacts (https://world.openfoodfacts.org) a free and online database of nearly 2 million food products around the world. This data contains metadata of packaged foods such as Name, Brand, Product Image, Origin, Nutrition facts, Ingredients, Nutriscore, Nova-grade, etc.

For the purpose of this project, only packaged foods from United States were chosen to analyze their ingredients in English, and the number of items were around 190,000 products, along with 12 numerical and categorical features and 2 targets

## PROJECT DESCRIPTION
   - ```Project_Files/Novous_Preprocessing.ipynb```: Data Preprocessing Notebook for EDA, ML pipelines and Recommendation system
    
   - ```Project_Files/Novous_EDA.ipynb```: This notebook contains some insights about Nutrition of most Packaged food products in the United States and how they can impact our health
    
   - ```Project_Files/Novous_Classification.ipynb```: Machine Learning model to classifify the Processing level of packaged food products
    
   - ```Project_Files/Novous_Regression.ipynb```: This notebook contains Regression models to predict the Nutrition scores of packaged foods
    
   - ```Project_Files/Novous_AdditivesOCR.ipynb```: Implementation of OCR for identifying additives listed in the packaged food labels 
    
   - ```Project_Files/Novous_Recommendation.ipynb```: Recommendation system that utilizes Content-based Filtering to recommend healthier substitution that priorities health and food quality
    
   - ```app.py```: Streamlit web app
   
## REQUIREMENTS
   - streamlit 0.81.1
   - sklearn 0.22.2.post1
   - tesseract
   - pytesseract
   - nltk 3.5
   - plotly
   - imblearn 0.7
   - opencv

## OUTLINE
1. Defining Questions
2. Data Selection & Processing
3. Explorative Data Analytics
4. Developing Models
    - Classification & Regression Models
    - OCR for Additives Detection
    - Recommendation System
5. Fine-tuning & Evalutation


### I. Questions 
- NOVA-grade (processing level of food) - Common ingredients/food that are classified as most processed

- Nutrition-grade - Is the food really nutritious as its label mentions?

- How to choose similar products to my favorite one that has the best nutritional quality and as less processing as possible?

### II. Data Pre-processing
**1. Filtering unescessary columns and data**

**2. Dealing with missing data**

   - For Recommendation system: data with missing Nutri-score and Nova-grade targets are filled in using previously built models to increase the number of items for Recommendation
    
   - For Classification and Regresison tasks, products with missing values are removed
    
**3. Outliers Treatment**

   - Any numerical values whose values are outside of quantile 0.99 are removed for Classification & Regression
    
   - However, for Data Analysis, these outliers are retained to gather insights
    
**4. Regular Expression & String Manipulation**

   - For Recommendation system, the products need to be grouped into Categories and Labels. In addition, before feeding into TfidfVectorizer, the categorical features need to undergo some Regular expression and string manipulation to clean the special characters, replace comma with space, and finally joining multiple words in the same ingredient by a hyphen. After transformation, each product's ingredients collection is represented as a string of multiple ingredients.

Sample result:

<img src="https://github.com/thuminhle59/Novous_EatBetterNotLess/blob/main/imgs/reg.png?raw=true" width="800"/>


### III. Explorative Data Analysis

**1. Overview of Packaged Food Quality**

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/nutri.png" width="600"/>

**About 70% of packaged foods from United States are heavily processed (NOVA 4).
This number is very consistent with most published reports of fast food in United States. Only a very smaller portion of food is unprocessed or minimally procssed.**

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/nova.png" width="600"/>

**Regarding Nutri-grade, nearly 50% of foods are given grade of D or E, this means most packaged food products do not bring many health benefits to consumers at all.**

**2. Vegan vs. Non-Vegan**

 **Does Vegan equal Healither?**

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/veg_nutri.png" width="600"/>

**Are Vegan Foods less processed?**

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/vegnova.png" width="600"/>

**With 98% of Non-Vegan foods fall into NOVA-grade D or E (foods with high level of processing). So why not consider going Vegan?**

**3. Additives**

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/adds.png" width="300"/>

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/add_cat.png" width="800"/>

**Most packaged foods contain at least some additives added for coloring, preservative, or emulsifiers. In 1 package of Dessert, there could be up to 35 additives which definitely do more harm than good to our health.**


### IV. Developing Models

**1. Random Forest for NOVA-grade Classification and Nutri-score Regression**

  - Classification Benchmark Result: 

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/classification.png" width="600"/>

   - Regression Benchmark Result:
    
<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/regression.png" width="600"/>

Random Forest was chosen as the Final model for both Classification and Regresison tasks.

**Streamlit Demo**

![grading](https://github.com/thuminhle59/Novous_EatBetterNotLess/blob/d88f07ed86ac9e5b7c82e818d18b539a2f5fe2fa/imgs/grading.gif)

**2. OCR for Additives Detection**

![additives_gif](https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/additives.gif)

When an image of ingredients is passed through Novous, with the help of Pytesseract and Regex, Novous can detect the additives in E-numbers and provide the information such as side effects and usages to users.

**3. Recommendation System with Content-based Filtering**

Tfidf Vectorizer is used to vectorize the categorical features into numbers. Each product will be a vector with each entry is a unique ingredient of that product. Tfidf highlights the important and unique ingredients and making sure that unimportant ones (water, sugars, etc..) do not dominate


### V. Fine-Tuning & Evaluation

**Fine-tuning Result**

||Random Forest Classifier|Random Forest Regressor|
|-------|---------|---------|
|Roc Auc| 0.94228 |    NA   |
|MAE    |   NA    | 0.49874 |

Roc Areas for each NOVA-grade class

<img src="https://raw.githubusercontent.com/thuminhle59/Novous_EatBetterNotLess/main/imgs/roc_auc.png" width="600"/>

## KEY TAKEAWAYS

The 2 Machine Learning models can predict and classify the Nutritional Value as well as Processing levels of packaged foods just using the Nutrition facts on the packaged food labels. It is also able to detect any Additives in the Ingredients list that are written under E-codes. In addition to Food Quality assessment features, the Recommender system that uses Tfidf will suggest a cleaner and better food substitution for people to improve their health.

From the Data Analysis done on packaged food products, I do think that Vegan foods have better nutritional quality than most foods that are Non-vegan. In addition, by consuming Vegan food, consumer will have lower chance of getting heavily-processed foods that could do great damage to their health and increase risks of cardiovascular diseases. However, since most packaged foods are loaded with additives for coloring, preservative, or emulfiers, etc., I do recommend that we should limit fast foods, and stick with home-made meals, especially those from fruits, vegetables, grains, legumes or plant-based proteins.

## FUTURE WORK

1. OCR of Nutrition Fact labels on Packaged Foods for automatic input of Food-quality assessment
2. Personalized Allergens Detection using OCR and String matching
3. More Nutrition Analysis
4. Implementation on Cosmetics Products using similar approaches

