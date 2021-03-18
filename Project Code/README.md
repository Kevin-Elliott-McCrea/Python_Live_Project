# Django Web Application Code Base


## Story 1 - Create Model, database and other connecting stuff??

Here I added my application to the settings.py file in the main part of the website code (what do I call this?)

```python

```

## Story 2 - Make Base Page and Home Page

#### Base Page View

This is used as a template for postitioning html elements and importing libraries/frameworks in all webpages in my web app
```python
{% load static %}
<!DOCTYPE html>
<html lang="en">
    <head>
    {% block head %}
        <meta charset="UTF-8">
        <title>{% block title %}{% endblock %}</title>
        <!-- This is where we set the styling for all the html pages -->
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
        <link href="https://fonts.googleapis.com/css?family=Roboto" rel="stylesheet">
        <link href="//fonts.googleapis.com/css?family=Lobster&subset=latin,latin-ext" rel="stylesheet" type="text/css">
        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous">

        <!-- Bootstrap JS, Popper.js, and jQuery -->
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
    {% endblock %}
    {% block css %}
        <!-- Non-bootstrap styling imported here -->
        <link rel="stylesheet" type="text/css" href="{% static 'FoodRecipeApp/css/navbarMain.css' %}">
        <link rel="stylesheet" type="text/css" href="{% static 'FoodRecipeApp/css/footerMain.css' %}">
        <link rel="stylesheet" type="text/css" href="{% static 'FoodRecipeApp/css/main.css' %}">
    {% endblock %}
    </head>
    <body>
    <!-- Navbar and footer are in separate files to account for scaling up in size of website -->
    {% include "FoodRecipeApp/FoodRecipeApp_Navbar.html" %}
            <div class="body_container">
                <header class="header-title">
                    <h1>{% block header %}{% endblock %}</h1>
                </header>
                {% block content %}{% endblock %}
            </div>
    {% include "FoodRecipeApp/FoodRecipeApp_footer.html" %}
    </body>
</html>
```

#### Home Page View

Since I only have one line of css for the home page, I will just show the html and template language here
```python

{% extends "FoodRecipeApp/FoodRecipeApp_base.html" %}

{% load static %}


{% block title %}Recipes with Nutrition{% endblock %}


{% block header %}

<div><h2 class="header-txt">Discover new recipes and know if they're healthy!</h2></div>
<div><h3 class="header-txt">- Click the navbar to explore!</h3></div>

{% endblock %}
```


## Story 3 - Make Navbar and Footer

Here I struggled to understand how to use template tags to set up links from the navbar to other pages in my app. After a good chunk of time, I figured it out with the help of the instructors and styled the navbar and footer. Then I used the "extends" template tag to allow the base.html page to inherit the footer and navbar. Since the base.html page is extended in each page of my site area, the navbar and footer is also in each one.

#### Navbar Template

I kept the navbar simple here, as I wasn't going to have a huge site to navigate through
```python
{% load static %}

{% block list %}
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

    <!-- This is extended in all webpages -->
    <div class="topnav">
      <a href="{% url 'FRhome' %}" class="active">Home</a>
      <a href="{% url 'FRcreate' %}">Create Recipes</a>
      <a href="{% url 'FRshowRecipes' %}">See Your Recipes</a>
    </div>

{% endblock %}
```

#### Navbar CSS

Here I wanted the links to span the entire height of the navbar and be aligned on the left of the screen. I also added hover effects.
```CSS
.topnav {
  background-color: #333;
  overflow: hidden;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;
  width: 100%;
  height: 45px;
}

/* Style the links inside the navigation bar */
.topnav a {
  float: left;
  display: block;
  color: #f2f2f2;
  text-align: center;
  padding: 10px 12px;
  text-decoration: none;
  font-size: 17px;
}

/* Change the color of links on hover */
.topnav a:hover {
  background-color: #ddd;
  color: black;
}

/* Add an active class to highlight the current page */
.topnav a.active {
  background-color: #4CAF50;
  color: white;
}

/* Hide the link that should open and close the topnav on small screens */
.topnav .icon {
  display: none;
```


#### Footer Template

Added to round out the site formatting.
```python
{% load static %}

<section class="footer">
    <p class="footer-text">&copy;2020 - Nutrition in Recipes</p>
</section>
```

#### Footer CSS

This was just a basic footer. Made transparent and with text aligned in the center.
```CSS
body {
    height: 100%;
    margin: 0;
}

.footer {
  opacity: .85;
  background-color: #d3d3d3;
  padding: 5px 5px 5px 5px;
  width: 100vw;
  border-radius: var(--border-radius) var(--border-radius) 0px 0px;
  margin: 0 0 0 0;
  bottom: 0;
  height: 2.2rem;
  position: fixed;
  }

.footer-text {
  text-align: center;
  color: #000000
}
```


## Story 4 - Make Create, Edit Page and Delete Page

After styling the create page, I realized that I can reuse the code for the edit and delete pages as well, while keeping the style looking good. This adds to the efficiency of the program and is quicker to code as well.

#### Create Page View

Created with easy UI for user to add their own recipe. All fields must be filled out or you will get an error upon submitting.
```python
{% extends "FoodRecipeApp/FoodRecipeApp_base.html" %}
{% load static %}


<!-- This is a basic create recipe page -->
{% block content %}
<div class="jumbotron jumbotron-crud-form">
    <form action="" method="post">
        {% csrf_token %}
        <table>
            {{ form.as_table }}
        </table>
        <input type="submit" value="Submit">
    </form>
</div>
{% endblock %}
```

#### Edit Page View

This has the same formatting as the create page, but it adds a button that gives the option to delete a recipe.
```python
{% extends "FoodRecipeApp/FoodRecipeApp_base.html" %}
{% load static %}


{% block content %}
    <!-- This is a table that renders a single recipe so that it can be edited -->
    <div class="jumbotron jumbotron-crud-form">
        <form method="POST">
            {% csrf_token %}
            <table>
                {{ form.as_table }}
            </table>
            <input type="submit" value="Submit changes">
        </form>
    </div>

    <!-- This links to the delete confirmation page -->
    <div class="button-container">
        <a href="{% url 'FRdeleteRecipe' pk %}"><button type="button" class="btn btn-primary button-align">Delete Recipe</button></a>
    </div>

{% endblock %}
```

#### Delete Page View

This was added to make sure the user understands that they are deleting something, before they complete the process.
```python
{% extends "FoodRecipeApp/FoodRecipeApp_base.html" %}
{% load static %}



{% block content %}

    <div class="jumbotron jumbotron-crud-form">
        <form method="POST">
            {% csrf_token %}
            <h3 class="">Do you want to delete the recipe "{{ recipe.title }}"?</h3>
            <!-- This completes the delete and brings user back to all recipes -->
            <div class="button-container">
                <p class="button-align"><input class="btn btn-danger" type="submit" value="Yes">  <a class="btn btn-success" href='../../../'>Cancel</a></p>
            </div>
        </form>
    </div>

{% endblock %}
```

#### CSS For All Three Pages

This is intentionally very economical. I used very little CSS but still got the job done. The home page uses only the jumbotron crud form selector, but the edit and delete pages also use the button container and button align css selectors.
```CSS
.jumbotron-crud-form {
 width: 35%;
 opacity: .8;
 margin: auto;
}

.button-container {
 height: 38px;
 position: relative;
}

.button-align {
 margin: 0;
 position: absolute;
 top: 50%;
 left: 50%;
 -ms-transform: translate(-50%, -50%);
 transform: translate(-50%, -50%);
}
```

## Story 5 - Make Index Page

#### Index Page View

Most of the difficulty here came from figuring out the template tags needed to loop through the model and bring each recipe in as a form. Once I figured that out, I let the bootstrap do the rest of the work for styling.
```python
{% extends 'FoodRecipeApp/FoodRecipeApp_base.html' %}

{% block content %}
  <!-- The styling is mostly bootstrap. I renders details from the database using template tags for each recipe in boxes -->
  <div class="manage-containers">
    <div class="list-group">.
      {% for recipe in recipe_list %}
      <!-- The whole container is a link to the details of that individual recipe -->
      <a href="recipeDetails/{{ recipe.id }}/" class="list-group-item list-group-item-action flex-column align-items-start manage-containers">
        <div class="d-flex w-100 justify-content-between">
          <h5 class="mb-1">Recipe name: {{ recipe.title }}</h5>
        </div>
        <p class="mb-1">Description: {{ recipe.description }}</p>
      </a>
      {% endfor %}
    </div>
  </div>
{% endblock %}
```

#### Index Page CSS

I keep this CSS very short, as I used bootstrap classes to good effect for styling.
```CSS
.manage-containers {
 opacity: .92;
 width: 55%;
 margin: auto;
}
```

