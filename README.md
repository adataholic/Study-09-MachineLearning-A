# Study-09-MachineLearning-A

----------------------------------------------------------------------------------------------------------------------------------------
### Warming-Up
> 1. If our **df** has columns(x1, x2, y), we need to split the input and output into Numpy Arrays, in order to apply the classifiers in **scikit learn**...saying that..we convert a **Series** into a **NumpyArray**.
```
X = np.array(df[['x1','x2']])
y = np.array(df['y'])
```
> 2. **Train** models in **sklearn**: `classifier.fit()`
```
from sklearn.linear_model import LogisticRegression
classifier = LogisticRegression()
classifier.fit(X,y)

from sklearn.tree import DecisionTreeClassifier
classifier = DecisionTreeClassifier()
classifier.fit(X,y)

from sklearn.svm import SVC
classifier = SVC()
classifier.fit(X,y)

from sklearn.neural_network import MLPClassifier
classifier = MLPClassifier()
classifier.fit(X,y)
```
<img src="https://user-images.githubusercontent.com/31917400/39083317-9f985d68-455a-11e8-9e54-426359e1c486.jpg" />

Logistic Regression didn't do so well, as it's a linear algorithm. Decision Trees and SVM managed to bound the data well, but..what about this? 
Let's play with some of these parameters of SVM and tune them in such a way that they bound the desired area! The kernel that works best here is 'rbf', with large values of 'gamma'.
 - **kernel**(string): 'linear', 'poly', 'rbf'.
 - **degree**(integer): This is the degree of the 'polynomial' kernel only.
 - **gamma**(float): The gamma parameter that goes with 'rbf' kernel only.
 - **C**(float): The C parameter.
```
classifier = SVC(kernel = 'rbf', gamma = 200)
classifier.fit(X,y)
```
> 3. Validation-Prep (data splitting)
 - Regression: it predicts or returns a **value**
 - Classification: it determines or returns a **state**(+/-, Y/N, Cat/Dog/Bird...where the data-pt belongs to..)
<img src="https://user-images.githubusercontent.com/31917400/39257585-cac6de22-48a9-11e8-8f45-1bad945142f6.jpg" />

## Split...`train_test_split(X, y, test_size)`
 - X_train: The training input
 - X_test: The testing input
 - y_train: The training labels
 - y_test: The testing labels
```
X = np.array(data[['x1', 'x2']])
y = np.array(data['y'])
from sklearn.cross_validation import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.25)
```
> 4. Validation with **Confusion-Matrix**
### How well is my model doing ? 
<img src="https://user-images.githubusercontent.com/31917400/39307945-1e1d187c-495c-11e8-8da5-d29e27b618b6.jpg" />

## Metric_01: Accuracy...`accuracy_score(y_true, y_pred)` 
```
from sklearn.metrics import accuracy_score

accuracy_score(y_true, y_pred)
```
---------------------------------------------------------------------------------------------------------------------------------------
### But..when Accuracy won't work ?
<img src="https://user-images.githubusercontent.com/31917400/39308440-594fbf20-495d-11e8-97f5-cd51d15696d7.jpg" />

## Metric_02: Precision, Recall and F_Beta Score
Plus, between these two errors, sometimes, depending on situation, the one is more critical over others (FP vs FN)
 - Precision (to capture **FP** and avoid): Out of all data-pt our model diagnosed with **Positive** world, how many did our model classify correctly ? 
 - Recall (to capture **FN** and avoid): Out of all data-pt that are actually **positive**, how many did our model classify correctly ? 
<img src="https://user-images.githubusercontent.com/31917400/39315393-7321c1a8-496e-11e8-8875-20948e25ceab.jpg" />

#### a) F1-Score (Precision ~ Recall)
 - We can combine these two metrics into one metric, using **'Harmonic Mean'** which is called **'F1-Score'**(2xy/x+y)
 - F1-Score is closer to the **smallest** b/w Precison and Recall. If one of them is particularly low, the F1-Score kind of raises a flag ! 
<img src="https://user-images.githubusercontent.com/31917400/39317672-15d0cf0c-4974-11e8-90e7-a950a87be5e2.jpg" />

#### b) F_Beta-Score (Precision with 'FP' vs Recall with 'FN')
 - When our model care a bit more about the one than the other, we want sth more skewed towards the one.
 - Select Beta !!! 
<img src="https://user-images.githubusercontent.com/31917400/39332689-208dfa1a-49a0-11e8-9d33-d9d7f53a1626.jpg" />

 - Finding a good Beta requires a lot of intuition of our data. For example,
   - Detecting malfunctioning parts in a spaceship ?--(FN Warning: a high recall model): Beta=2
   - Sending phone notifications about videos a user may like ?--(not much costly: a decent precision and a decent recall): Beta=1
   - Sending promotional material in the mail to potential clients ?--(costly, so FP Warning: a high precision model): Beta=0.5 

## Metric_03: Roc-Curve (Receiver Operating Characteristic)
 - In the chart of "TPr vs FPr", **the area** under the curve is our metric value. 
 - Consider the data which is now one dimensional, so all the red, blue pt lie in 1 line and we want to find the correct **split**.
<img src="https://user-images.githubusercontent.com/31917400/39334203-9d835dc6-49a5-11e8-983d-bc43a81043c0.jpg" />

 - How to construct those values?
<img src="https://user-images.githubusercontent.com/31917400/39336183-0e435324-49ae-11e8-8993-38076294c030.jpg" />













































































































