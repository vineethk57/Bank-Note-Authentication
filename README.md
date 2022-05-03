
# Bank note authentication 

Bank note authentication, a kaggle problem is converted into an end to end project.

The steps followed will be:
1. Bank note authentication with machine learning
2. Building a flask app 
3. Deployment using flask and flassger
4. Deployment using dockers and flask
5. Deployment using Streamlit library


## Dataset

Data were extracted from images that were taken from genuine and forged banknote-like specimens. For digitisation, an industrial camera usually used for print inspection was used. The final images have 400x 400 pixels. Due to the object lens and distance to the investigated object gray-scale pictures with a resolution of about 660 dpi were gained. Wavelet Transform tool were used to extract features from images.

https://www.kaggle.com/datasets/ritesaluja/bank-note-authentication-uci-data

Dataset can be used for Binary Classification sample problems

<img width="430" alt="1" src="https://user-images.githubusercontent.com/30193984/166441295-f472c8ae-97d9-4b4e-b9c9-09201866bc7e.png">

Dataset contains 1372 rows × 5 columns, where class 1 represents authentic banknote and class 0 represents fake banknotes.

    


## 1. Bank note authentication with machine learning

NOTE: Since the aim of this project is to understand various deployment methods. The dataset wouldn't be pre-processed like using normalisation techniques nor any performance enhancing techniques.

1. Dataset is loaded using Pandas().
2. Independent and Dependent features are separated
3. Train test split is achieved using sklearn()
4. Model is trained using random forest classifier
5. Predictions and accuracy of predictions are checked.
6. Classifier is saved using Pickle()

"ModelTraining.ipynb" contains all the operations mentioned above.
Also "classifier.pkl" contains the saved model.
## 2. Building a Flask app 

What is Flask?
<src="https://flask.palletsprojects.com/en/2.1.x/_images/flask-logo.png">
Flask is a micro web framework written in Python. It is classified as a micro-framework because it does not require particular tools or libraries. It has no database abstraction layer, form validation, or any other components where pre-existing third-party libraries provide common functions.

Flask app developed here has 3 interfaces

1. Welcome page
A function is created for a welcome page.

Screenshoot Welcome

2. Prediction using get().

A function is created for requesting the values of dependent features for prediction.

Screenshoot prediction

3. Prediction using Postman.

Postman is an application used for API testing. It is an HTTP client that tests HTTP requests, utilising a graphical user interface, through which we obtain different types of responses that need to be subsequently validated.

Both get() and post() method can be used in postman.

3.1. Using get().

Here the values will be passed as input same as the previous function but there will be a graphical user interface. 

Screenshoot get()

3.2. Using post().

Here the test file will be given as output.

Screenshoot post()

## 3. Deployment using flask and flassger

What is Flasgger?

Flasgger is a Flask extension to extract OpenAPI-Specification from all Flask views registered in your API.

Flasgger also comes with SwaggerUI embedded so you can access http://localhost:5000/apidocs and visualize and interact with your API resources.

Flasgger also provides validation of the incoming data, using the same specification it can validates if the data received as as a POST, PUT, PATCH is valid against the schema defined using YAML, Python dictionaries or Marshmallow Schemas.

GitHub: https://github.com/flasgger/flasgger 

Welcome screenshot

1. Using get().

UI for input

UI for ouput


2. Using post().

UI for input

UI for ouput

## 4. Deployment using dockers and flask

What is Docker and why it is used?

Docker is an open source containerisation platform. It enables developers to package applications into containers—standardized executable components combining application source code with the operating system (OS) libraries and dependencies required to run that code in any environment.

A 3-step process followed:
1. Create a docker file.

Docker file is created inside the working directory with the following commands.
```bash
FROM continuumio/anaconda3:4.4.0
COPY . /usr/app/
EXPOSE 5000
WORKDIR /usr/app/
RUN pip install -r requirements.txt
CMD python flask_api.py
```
requirements.txt contains the following commands
```bash
Flask==1.1.1
gunicorn==19.9.0
itsdangerous==1.1.0
Jinja2==2.10.1
MarkupSafe==1.1.1
Werkzeug==0.15.5
numpy>=1.9.2
scipy>=0.15.1
scikit-learn==0.22.1
matplotlib>=1.4.3
pandas>=0.19
flasgger==0.9.4
streamlit
```
2. Build the docker image

2.1. Create docker image
```bash
docker build -t money_api .
```
Screenshot 

2.2. View created image
```bash
docker ps
```
Screenshot

3. Run the docker image
```bash
docker run -p 8000:8000 money_api
```
Screenshot

Access it using the IP address in which the docker is configured.
```bash
192.168.99.100:8000/apidocs
```
Screenshot

## 5. Deployment using Streamlit library
What is the use of Streamlit?

Streamlit is an open source app framework in Python language. It helps us create web apps for data science and machine learning in a short time. It is compatible with major Python libraries such as scikit-learn, Keras, PyTorch, SymPy(latex), NumPy, pandas, Matplotlib etc.

https://streamlit.io/

Run app1.py using:
```bash
streamlit run app1.py
```
Screenshot

Screenshot

