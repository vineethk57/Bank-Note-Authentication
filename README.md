
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
![flask-logo](https://user-images.githubusercontent.com/30193984/166443087-520880fd-3c6e-4e22-b368-ee58a8735dea.png)

Flask is a micro web framework written in Python. It is classified as a micro-framework because it does not require particular tools or libraries. It has no database abstraction layer, form validation, or any other components where pre-existing third-party libraries provide common functions.

Flask app developed here has 3 interfaces

1. Welcome page
A function is created for a welcome page.

<img width="978" alt="welcome" src="https://user-images.githubusercontent.com/30193984/166443324-e074c5ae-45b7-497e-a1d8-9928a758a665.png">


2. Prediction using get().

A function is created for requesting the values of dependent features for prediction.

<img width="976" alt="get()" src="https://user-images.githubusercontent.com/30193984/166443398-3dd25c37-ca05-4279-8e12-5e6c11c18598.png">

3. Prediction using Postman.

Postman is an application used for API testing. It is an HTTP client that tests HTTP requests, utilising a graphical user interface, through which we obtain different types of responses that need to be subsequently validated.

Both get() and post() method can be used in postman.

3.1. Using get().

Here the values will be passed as input same as the previous function but there will be a graphical user interface. 

<img width="875" alt="postman get" src="https://user-images.githubusercontent.com/30193984/166443443-afc1fa85-efcb-4650-bca3-39ba44a11608.png">


3.2. Using post().

Here the test file will be given as output.

<img width="873" alt="postman post" src="https://user-images.githubusercontent.com/30193984/166443469-8ecedf13-2e04-424d-8c17-767c6d7868a8.png">


## 3. Deployment using flask and flassger

What is Flasgger?![flasgger](https://user-images.githubusercontent.com/30193984/166443667-ddef7747-6af6-46c5-8e8d-019c3e548fe1.png)

Flasgger is a Flask extension to extract OpenAPI-Specification from all Flask views registered in your API.

Flasgger also comes with SwaggerUI embedded so you can access http://localhost:5000/apidocs and visualize and interact with your API resources.

Flasgger also provides validation of the incoming data, using the same specification it can validates if the data received as as a POST, PUT, PATCH is valid against the schema defined using YAML, Python dictionaries or Marshmallow Schemas.

GitHub: https://github.com/flasgger/flasgger 

Welcome screenshot

1. Using get().

UI for input

<img width="1102" alt="Flassger get" src="https://user-images.githubusercontent.com/30193984/166443739-60febb2e-4fbc-457d-8c89-451f5f5e166d.png">


UI for ouput

<img width="1102" alt="Flassger get out" src="https://user-images.githubusercontent.com/30193984/166443807-2b2b6a74-a26d-43e8-b531-b9c1f766c291.png">


2. Using post().

UI for input

<img width="1105" alt="Flassger post " src="https://user-images.githubusercontent.com/30193984/166443850-37049832-b8d3-4fe5-95f9-89337195fc00.png">


UI for ouput

<img width="1104" alt="Flassger post out" src="https://user-images.githubusercontent.com/30193984/166443874-f7066f4f-39e2-45e7-b6e0-6b9e8a583e47.png">

## 4. Deployment using dockers and flask

What is Docker and why it is used?![homepage-docker-logo](https://user-images.githubusercontent.com/30193984/166444178-592fecec-3fcd-46bd-af6e-36a7c89ce76a.png)

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
<img width="857" alt="Docker build" src="https://user-images.githubusercontent.com/30193984/166451574-006dde05-5dda-4bc9-90d4-00bdf8a0d3de.png">


2.2. View created image
```bash
docker ps
```
<img width="899" alt="Docker view" src="https://user-images.githubusercontent.com/30193984/166451661-d715249c-8fb8-4bfc-b710-f7bc14b25de1.png">


3. Run the docker image
```bash
docker run -p 8000:8000 money_api
``` 
<img width="876" alt="Docker run" src="https://user-images.githubusercontent.com/30193984/166451692-d2471b15-7c7e-4407-ad85-011e4cd454e8.png">

Access it using the IP address in which the docker is configured.
```bash
192.168.99.100:8000/apidocs
```
Screenshot

## 5. Deployment using Streamlit library
What is the use of Streamlit? ![1_u9U3YjxT9c9A1FIaDMonHw](https://user-images.githubusercontent.com/30193984/166455081-71b10354-c9fa-4270-b3d9-053d2b2de382.png)

Streamlit is an open source app framework in Python language. It helps us create web apps for data science and machine learning in a short time. It is compatible with major Python libraries such as scikit-learn, Keras, PyTorch, SymPy(latex), NumPy, pandas, Matplotlib etc.

https://streamlit.io/

Run app1.py using:
```bash
streamlit run app1.py
```
<img width="654" alt="Streamlit run" src="https://user-images.githubusercontent.com/30193984/166455121-ffbe7c2c-1c3d-4cc8-86b8-7e529861fb9b.png">

<img width="631" alt="streamlit app" src="https://user-images.githubusercontent.com/30193984/166455184-b6164bbc-eb0e-4b7a-8042-be95336fe694.png">


