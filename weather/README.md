# Weather Report
------------

## Description:

This is the weather application that displays weather information based on the location.
          
### Front End:

The user enters the city name in the text box. An API call is made from open weather map API (https://openweathermap.org). 

To fetch the required information we need to signup and get the appid key associated with your account. Copy the appid key in app.py file to get the weather report.

* weather.html is used to plot the data fetched from the API.
* It displays the City name, weather report and the description of the weather.

### Back End:

Flask framework is used to build the backend of the application. It uses the OpenWeatherAPI to fetch the weather data.

### Cloud:

Used Google Cloud Platform to deploy the application on VM instance.


### Prerequisites:

To deploy the application in Google Cloud Platform we need to have some packages installed in the instance. Here are the list of packages we need to install.

* Python: We need to make sure that the Python development, including developing Python applications that run on Google Cloud Platform (GCP).

* **pip:** pip is a package management system used to install and manage software packages written in Python.

* **Flask:** Flask is a lightweight WSGI web application framework.

* **Flask-SQLAlchemy:** Flask-SQLAlchemy is an extension for Flask that adds support for SQLAlchemy to your application.

* **Requests:** Requests is the only Non-GMO HTTP library for Python.

* **Sqlite3:** sqlite3 drivers for the 'db' library.

