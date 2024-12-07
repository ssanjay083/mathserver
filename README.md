# Ex.05 Design a Website for Server Side Processing
# Date:18.10.2024
# AIM:
To design a website to calculate the power of a lamp filament in an incandescent bulb in the server side.

# FORMULA:
s = d/t
s = speed
d = distance in km
t = time taken in hours
# DESIGN STEPS:
## Step 1:
Clone the repository from GitHub.

## Step 2:
Create Django Admin project.

## Step 3:
Create a New App under the Django Admin project.

## Step 4:
Create python programs for views and urls to perform server side processing.

## Step 5:
Create a HTML file to implement form based input and output.

## Step 6:
Publish the website in the given URL.

# PROGRAM :
speed.html
```
<!DOCTYPE html>
<html>
<head>
    <title>Speed Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #89f7fe, #66a6ff);
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: #fff;
            padding: 20px 30px;
            border-radius: 10px;
            box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            text-align: center;
        }
        h1 {
            color: #4A90E2;
            margin-bottom: 20px;
        }
        label {
            display: block;
            font-weight: bold;
            margin-bottom: 8px;
        }
        input {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            background-color: #4A90E2;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #357ABD;
        }
        .result, .error {
            margin-top: 20px;
            font-size: 18px;
            padding: 10px;
            border-radius: 5px;
        }
        .result {
            background-color: #e8f8e8;
            color: #4CAF50;
        }
        .error {
            background-color: #f8e8e8;
            color: #F44336;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Speed Calculator</h1>
        <form method="post" action="/cal/">
            {% csrf_token %}
            <label for="distance">Distance (in km):</label>
            <input type="number" step="0.01" id="distance" name="distance" placeholder="Enter distance" required>
            
            <label for="time">Time (in hours):</label>
            <input type="number" step="0.01" id="time" name="time" placeholder="Enter time" required>
            
            <button type="submit">Calculate Speed</button>
        </form>

        {% if error %}
        <div class="error">{{ error }}</div>
        {% endif %}
        {% if speed %}
        <div class="result">
            <h2>Result:</h2>
            <p>Speed: {{ speed }} km/h</p>
        </div>
        {% endif %}
    </div>
</body>
</html>
```
views.py
```
from django.shortcuts import render

def calculate_speed(request):
    speed = None  # Initialize speed
    error = None  # Initialize error message

    if request.method == 'POST':
        try:
            # Retrieve distance and time from the POST request
            distance = float(request.POST.get('distance', 0))
            time = float(request.POST.get('time', 0))

            # Check if time is valid (not zero or negative)
            if time > 0:
                speed = round(distance / time, 2)  # Calculate speed and round to 2 decimal places
            else:
                error = "Time must be greater than zero."
        except ValueError:
            error = "Please enter valid numbers for distance and time."

    return render(request, 'speed.html', {'speed': speed, 'error': error})
```
urls.py
```
from django.contrib import admin
from django.urls import path
from calculator import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('cal/',views.calculate_speed ,name="calculate_speed" ),  # Include the URLs from the app
]
```
# SERVER SIDE PROCESSING:


![Screenshot 2024-12-07 133830](https://github.com/user-attachments/assets/835d936a-d9de-4471-9a55-d0b5bd2f0949)




# HOMEPAGE:

![Screenshot 2024-12-07 133900](https://github.com/user-attachments/assets/6d8b74ea-1a72-4376-9a9a-3d03091d6bd8)



# RESULT:
The program for performing server side processing is completed successfully.
