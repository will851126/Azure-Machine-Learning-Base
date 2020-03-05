#  Natural language processing or Text analytics use Machine Learning Studio

## Scenario 
In this Lab ,you build a solution using [Machine Learning Studio](https://docs.microsoft.com/en-us/azure/machine-learning/studio/what-is-ml-studio) that predict movie reviews by  **Two-Class Logistic Regression Model** for IMDB Reviews dataset,This dataset contains the reviews and sentiment categories  of movies between years 2017 and 2018 in IMDB website with the corresponding reviews and emotional information.

You will learn text analytics using Machine Learning to create a model that will predict reviews' attributes and **Deploy model to Web Server**

###Reference: [Text Analysics](https://ithelp.ithome.com.tw/articles/10208700)

## Prerequisite
* Download *IMDb_Reviews.csv*  which is in this repository in your computer folder 

## Lab tutorial

### Create Machine Learning service workspaces 
* In Azure Portal Search for **Machine Learning Studio workspaces**, click **Add**.

<p align="center">
    <img src="https://i.imgur.com/33AXEdl.png" width="70%" height="70%">
    
#### Configure Resource information for **Machine Learning Studio workspaces**, click **DEVTEST Standard**. 

* For Workspace name, type a **Unique Name**

* Select **Resource Group** to organize your resource, if you don't have one, you can create a new resource group.

* For Location, choose `South Central US`

* For Storage account,select **Use Existing** to organize your Storage account,if you don't have one, you can Select a  **Create new**.

* For Workspace pricing tier,Choose `Standard`

* For Web service plan ,Choose `Create new`
   
<p align="center">
    <img src="https://i.imgur.com/NMkCExH.png" width="70%" height="70%">
    
### Launch Machine Learning Studio 

* From the list of vitural machine Learning studio workspaces, click **OverView**

* You can see **Additional Links**,Click `Launch Machine Learning Studio`

<p align="center">
    <img src="https://i.imgur.com/MZXVAA8.png" width="70%" height="70%">

### Create a Machine Learning Studio workspace

* Connect to **Azure Machine Learning Studio** Page

* Select your workspace in the upper-right-hand corner. 
* Click **Sign In**
   
### Upload a datasets
* Clicking **+NEW** at the bottom of the Machine Learning Studio window. 
* Select **Datasets**
* Click **FROM LOCAL FILE** Upload a new dataset from a local file

<p align="center">
    <img src="https://i.imgur.com/M9wS8S0.png" width="70%" height="70%">
    
* On select the data to upload,cilck **Choose File**,upload `IMDb_Reviews.csv`
* Enter a name for the dataset. For this tutorial, call it **IMDB Movie Review**
* For data type, select **Generic CSV File With no header (.nh.csv)**
* Import Dataset
<p align="center">
    <img src="https://i.imgur.com/2k11kZQ.png" width="70%" height="70%">

### Create an experiment

* Select **Experiment** at the bottom of the Machine Learning Studio window. Then click **Blank Experiment** to perpare our service.

<p align="center">
    <img src="https://i.imgur.com/8b6YyGJ.png" width="70%" height="70%">
    
* Select the default experiment name at the top of the canvas and rename **NLP Engine**

* Click the left side **Saved Datasets** > **My Datasets** > **IMDb_Reviews.csv**(Just add in folder), then drag the dataset to the workplaces.

<p align="center">
    <img src="https://i.imgur.com/H83UgOi.png" width="70%" height="70%">
    
* After we dragged it, click the output port of the **dataset** and select **Visualize**

<p align="center">
    <img src="https://i.imgur.com/wWXkZlo.png
" width="70%" height="70%">

* Click **sentiment** column, we can see our **missing values** is 0，fortunately we don't need to preprocess the missing values.

> Dataset：Collect movies reviews from IMDB website。**Review** is content detail, and **Sentiment** is labeled by hands, 1 is represented **Positive**, 0 is represented **Negative**
 
<p align="center">
    <img src="https://i.imgur.com/g9JGiwi.png
" width="80%" height="80%">

## Feature Engineering
[Feature engineering](https://en.wikipedia.org/wiki/Feature_engineering) is the process of using **domain knowledge** of the data to create features that make machine learning algorithms work

* Click the left side **Data Transformation** > **Manipulation** > **EditMetadata**, and drag it onto canvas
<p align="center">
    <img src="https://i.imgur.com/u75gkTP.png
" width="80%" height="80%">

* Click the output port of the dataset drag to the input port of Edit Metadata
<p align="center">
    <img src="https://i.imgur.com/UmuCsuv.png
" width="80%" height="80%">

### Edit Metadata
* Setting **Edit Metadata**：Click **Edit MetaData** > Select **Launch column selector** on the right side.
<p align="center">
    <img src="https://i.imgur.com/9pp9G46.png
" width="80%" height="80%">

* Continue to select **sentiment**, then click the right arrow click **Confirm**
<p align="center">
    <img src="https://i.imgur.com/6uGmXWY.png" width="80%" height="80%">
<p align="center">
    <img src="https://i.imgur.com/tak7WTv.png" width="80%" height="80%">

* Return to previous page, we change **Categorical** to **Make Categorical**
<p align="center">
    <img src="https://i.imgur.com/NWeftRY.png" width="80%" height="80%">

### Mapping Values

* We add a new component named **Group Categorical Values** in order to mapping '0' to 'Negative','1' to 'Positive'
<p align="center">
    <img src=" https://i.imgur.com/eycUbnj.png" width="40%" height="60%">

* Select the right side of Launch Column Selector
<p align="center">
    <img src="https://i.imgur.com/zOan8mX.png" width="80%" height="80%">

* Then, go to 'WITH RULES' > 'NO COLUMNS' > **Include** > **column names** > select **sentiment**
<p align="center">
    <img src="https://i.imgur.com/7Qsn2os.png" width="80%" height="80%">
* Return to previous page, make setting about the following information
<p align="center">
    <img src="https://i.imgur.com/Hpsr0d0.png" width="80%" height="80%">

* Finish that, we try to click 'RUN' on the bottom of the page to make sure without error.

* Click Right and **Visualize** our output.
<p align="center">
    <img src="https://i.imgur.com/JFVmPw1.png" width="80%" height="80%">
    
* You can see we transfer label to word categories.
<p align="center">
    <img src="https://i.imgur.com/jKB0I5s.png" width="80%" height="80%">


## Text Analysics
* Create Preprocess Text component from the left side, and drag onto our canvas.

<p align="center">
    <img src="https://i.imgur.com/DZ6mUEm.png" width="80%" height="80%">
    
* Look for **Preprocess Text Component** Detail
<p align="center">
    <img src="https://i.imgur.com/ag0FhW5.png" width="80%" height="80%">

* After we **RUN** our components now, we can see the different before we do preprocessing.

### Create training and test datasets

* Find the **Split Data** module, drag it onto the canvas, and connect it to the **Preprocessing Text** module

<p align="center">
    <img src="https://i.imgur.com/qUEND6D.png" width="70%" height="70%">

* In the Properties pane to the right of the canvas, click:

    * Split model:`Spilt Rows`

    * Fraction of rows in the first output dataset:`0.7`

    * Random seed: `0`

    * Stratified split:`False`

    <p align="center">
    <img src="https://i.imgur.com/UMAhPL1.png" width="60%" height="60%">

* Add **Extract N Grams Feature** from the left side（**Text Analytics** > **Extract N-Gram Features**

<p align="center">
    <img src="https://i.imgur.com/Ug6HEki.png" width="80%" height="80%">
    
* Settings:   
  	* Text column: Select `Preprocessed review`
  	
  	* Vocabulary mode: `Create`
  	
  	* N-Grams size: `3`
  	* Weighting funtion: `TF-IDF Weight`
  	* Feature scoring method: `Chi Squared`
  	* Number of desired features: `1000`
  	
  	<p align="center">
    <img src="https://i.imgur.com/k4Z5BAC.png" width="30%" height="70%"> 
    
* We can click **RUN** on the bottom of the page. And see the data visualization.
<p align="center">
    <img src="https://i.imgur.com/8TojlJm.png" width="70%" height="70%">
    
* Go back to previous page, we save the dataset in **Extract N Grams Feature** the second output, we'll use later.

<p align="center">
    <img src="https://imgur.com/nAc69wR.png" width="70%" height="70%">

* Add a new component from the left side named **Select Columns in Dataset**(Data Transformation > Select Columns in Dataset）because of only need parts of columns, and connect it to the **Extract N-Grams** module

* Click the right side **Select Columns** > **WITH RULES** > **ALL COLUMNS** > **Exclude** > **column names** : Review/Preprocessed Review/NumUniqueNGrams/NGramString

### Train Model 
The **Train Model** in Azure Machine Learning Studio to train a classification or regression model. Training takes place after you have defined a model and set its parameters, and requires tagged data.


* In the module palette, expand the **Machine Learning** category to the left of the canvas 

* Expand Initialize Mode

* select the **Two-Class Logistic Regression** module under the **Regression category**, and drag it to the experiment canvas


* Find and drag the Train Model module to the experiment canvas. Connect the output of the **Two-Class Logistic Regression** module to the left 

* Input of the Train Model module, and connect the output of the **Split Data**  to the right input of the **Train Model**

<p align="center">
    <img src="https://i.imgur.com/DaD6PHw.png" width="80%" height="80%">

* Select the column **Sentiment** from the right side
<p align="center">
    <img src="https://i.imgur.com/IyGdh6n.png" width="80%" height="80%">

* **Run** the experiment

### Score and evaluate the models
 Use the testing data that was separated out by the Split Data module to score our trained models. you can then compare the results of the two models to see which generated better results

 Now that we've trained the model using 70 percent of our data, we can use it to score the other 30 percent of the data to see how well our model functions.

*  Find and drag the **Score Model**  to the experiment canvas

####  Evaluate Model

* Find the **Evaluate Model** module and drag it onto the canvas

<p align="center">
    <img src="https://i.imgur.com/ItLZVvK.png" width="80%" height="80%">
    
* We need to use other 30% data to verify testing data, you can copy the previous component we create, and revize the following setting information:

<p align="center">
    <img src="https://i.imgur.com/K7aROSU.png" width="80%" height="80%">
    
* We add **Select Columns in Dataset** again.（Data Transformation > Select Columns in Dataset）, select columns from the right side.

* In **WITH RULES** > **Exclude** > **column names** > (Review/Preprocessed Review/NumUniqueNGrams/NGramString), and connect to **Score model**

<p align="center">
    <img src="https://i.imgur.com/fUn52yb.png" width="80%" height="80%">

* We can visualize our evaluate model's result:

<p align="center">
    <img src="https://i.imgur.com/gthtiCa.png" width="80%" height="80%">
    
* This is ROC curve to represent our accuracy:

<p align="center">
    <img src="https://i.imgur.com/jK7cBRE.png" width="80%" height="80%">
    
### Prepare for deployment
To give others a chance to use the predictive model you've developed in this tutorial, you can deploy it as a web service on Azure.
* Convert the training experiment you've created into a predictive experiment

* Deploy the predictive experiment as a web service

### Convert the training experiment to a predictive experiment

To get this model ready for deployment, you need to convert this training experiment to a predictive experiment. This involves three steps

* Click **Set Up Web Service**,Select **Predicture Web Service**

<p align="center">
    <img src="https://i.imgur.com/OZqb9ms.png" width="70%" height="70%">

* Modules that were used for training are removed:

    * Split Data

    * Train Model

    * Linear Regression model

    * Evaluate Model

* The saved trained model is added back into the experiment

* Web service input and Web service output modules are added

* **Run** the experiment

### Deploy a web service


* Click **Deploy Web Service** below the canvas 
* Add the previous dataset name **'Extract N-Gram Features from TEXT'** we just create, and drag to the **Predictive experiment**

<p align="center">
    <img src="https://i.imgur.com/kFVNuro.png" width="70%" height="70%">
    
* Only remain **Read Only** mode in **'Extract N-Gram Features from TEXT'**, and make sure this **Use filter-based feature selection** to  **False**

<p align="center">
<img src="https://imgur.com/cxuntQE.png" width="70%" height="70%">   

* Also, make uncheck in **Append score columns** in Score Model

<p align="center">
<img src="https://imgur.com/NNKH7XP.png" width="70%" height="70%">   


* Click **RUN** the experiment
* If it runs successfully, click **Deploy web service**
on the bottom of page.

<p align="center">
    <img src="https://i.imgur.com/JIpuKcI.png" width="70%" height="70%">
    
* Fill the Service name you want and select the plan we create
* Click **Deploy**

<p align="center">
    <img src="https://i.imgur.com/46zlfyt.png" width="70%" height="70%">
    
* In BASICS Banner, we click the top of buttom **Test Web Service**

<p align="center">
    <img src="https://i.imgur.com/Ekmn0EL.png" width="70%" height="70%">





### Test  web service

* In the Azure Machine Learning Web Services portal, click **Test** at the top of the page
  
    * These are the same columns that appeared in the original credit risk dataset

    * Fill in the reviews ' This movie makes me sleepy... ' in Input 1:
    
<p align="center">
    <img src="https://i.imgur.com/kKuKRDi.png" width="70%" height="70%">
    
* Click **Test Request-Response**
* Other Test, Fill in the reviews ' This is inspiring!!! ', We can get the **Score Labels** & **Score Probability** to classify the word successfully.

<p align="center">
    <img src="https://i.imgur.com/CZmQIv1.png" width="70%" height="70%">

### Clean up resources
In the resource group,**Delete resource**

* Machine Learning Studio workspaces

* Machine Learning Studio web Service Plan

* Storage Account

### Conclusion

Congratulations! You now have learned how to:

* Use Machine Learning Studio

* Build a Machine Learning Model as can **Perdict** 

* About Big Data Process and  Analysis Knowledge

* Deploy model to Web Services

 