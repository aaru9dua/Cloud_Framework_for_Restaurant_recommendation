# Cloud_Framework_for_Restaurant_recommendation

<h1> Objective</h1>

The goal of making a cloud-based restaurant recommendation system is to provide personalized recommendations to users based on their preferences. This system uses advanced algorithms and machine learning techniques to analyze vast amounts of data, including user reviews, restaurant ratings, menus, location data, and other relevant factors to generate a list of recommended restaurants that meet the user's criteria.

<h1>Project Workflow</h1>

<img width="701" alt="Screenshot 2023-06-19 at 10 38 28 AM" src="https://github.com/aaru9dua/Cloud_Framework_for_Restaurant_recommendation/assets/46483403/73afcfb4-9fd3-4298-ac37-177aee4d2a7d">

<h1>Proposed Architecture</h1>
<b>1. Data Collection</b>
<p>After this initial exploration we moved to using a dataset on Kaggle, the Yelp Dataset, which was created by the Yelp team and contains five JSON files and a user agreement.Out of 5 JSON files, we picked business.json and review.json. We loaded the json files using pandas. One of the early challenges was the size of the data, for example the review.json is a huge file (5 GB), and so we had to update our strategy to reduce the size of our dataset. We did this by filtering down to just the restaurant data, filter to 5 reviews per restaurant, and also filtering to just one city which had the majority of data. This reduced dataset was then uploaded as a dataset on Azure cloud.</p>

<b>2. Content based filtering</b>
<p>It is a type of recommendation based on restaurant’s informations like reviews or cuisine style. The steps involved in order to build this recommendation:
  
● Data reduction: Removed unnecessary columns from the merged Yelp dataset. Note: we are not taking location into consideration because that will be filtered once user’s will enter his/her desired state/city.<br>
● Feature engineering: Next, merge three columns : name, categories (cuisine) and reviews into a tag column to find the similarity between these textual informations.<br>
● Data Cleaning: We performed removing punctuations, lowering each word and removed the commoner morphological and inflexional endings from words using PorterStemmer library from NLTK and at last removed stop-words.<br>
● Data transformation: We Need To Convert Textual Data To A Numerical Value using CountVectorizer or TF-IDF. It focuses on the frequency of words and we set the maximum vocabulary size as 5000. We trained our pre-processes tag column in the feature extraction.<br>
● Similarity: The next step is to calculate a similarity score. We used Cosine similarity to calculate similarities between each restaurant’s description. <br>
● Get Recommendation: We build a function which takes in a restaurant name. It finds its index in the similarity list and sorts all its scores and gives us the top N (Let’s say 5) restaurant based on the user's choice.</p><br>

<b> 3. Deployment on Django Framework</b>
Install Django: Django is installed running pip command in the terminal: pip install Django. Make sure to have the latest version of pip installed.<br>
● Create a new Django project: To create a new Django project, run the following command in the terminal: django-admin startproject projectname.<br>
● Create a new Django app: In Django, a project can have multiple apps. To create a new app, run the following command in the terminal: python manage.py startapp appname.<br>
● Define models: Models are used to define the structure of the database. Define models in the models.py file in the app directory.<br>
● Create database tables: Run the following command in the terminal to create database tables for the models: python manage.py makemigrations and then python manage.py migrate.<br>
● Create a superuser: Run the following command in the terminal to create a superuser: python manage.py createsuperuser. Follow the prompts to create a username and password.<br>
● Start the development server: Run the following command in the terminal to start the development server: python manage.py runserver. This will start the server at http://localhost:8000/.<br>
● Once Django's setup is complete, we added our backend logic of filtering data for the recommendation in views.py and created recommendation.html and results.html to feed and show the output of the data being recommended.<br>
● Once the app was running we integrated and hosted it on Azure and before that uploaded the final framework on github.<br>


<b>4. Deployment on Cloud </b>
The following steps lead to our final website-<br>
1. Create an Azure Virtual Machine:<br>
● Log in to the Azure portal (portal.azure.com).
● Click on "Create a resource" and search for "Virtual Machine."
● Follow the prompts to configure the VM, including selecting the desired operating
system, size, and networking options.
● Set up SSH access during the VM creation process by providing a public SSH
key.<br>
2. Connect to the Azure VM via SSH:<br>
● Obtained the public IP address of the Azure VM from the Azure portal.
● Opened a terminal or SSH client on our local machine.
● Use the following command to connect to the VM:
ssh -i aarushidua aarushidua@20.231.108.199<br>
3. Install necessary dependencies on the Azure VM like Python packages.<br>
sudo apt install python3 python3-pip python3-venv git<br>
4.Next, Cloned our Django project repository into the Vm:<br>
Git clone https://github.com/aaru9dua/Cloud_Framework_for_Restaurant_recommendation.git<br>
5.Installed project dependencies by installing packages from requirement.txt file<br>
6.Started the Django development server on port 8000<br>
7. In our web browser, navigate to http://20.231.108.199:8000/, to see our website running successfully.<br>
   <img width="630" alt="Screenshot 2023-06-19 at 10 43 51 AM" src="https://github.com/aaru9dua/Cloud_Framework_for_Restaurant_recommendation/assets/46483403/d18d224d-8d38-4996-a193-214c4945f562">
