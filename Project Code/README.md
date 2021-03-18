# Django Web Application Code Base

I certaintly struggled a lot with this project, but especially so during the beginning phase. I talked to the instructors a lot to understand how to register filepaths in urls.py and the settings.py file. I also had a lot of trouble understanding how to use the model and model form to display that content on the template for the user to see. It was a huge difficulty, but I understood it well by the time I got to story 4 and it is now a tool under my belt. I also had a big difficulty with the template language, especially with how to use the tags: extends, includes, and the block tags. Once I figured that part out, the rest came with quite a bit more ease.

Here are the stories, with the code I used for them:

## Story 1 - Initialize Project. Make Base and Home Template.

First I started a new app with manage.py. Then I registered in the site settings.py file. From there, I created the base and home templates, along with the navbar and footer that would go into each template.

#### Base Template

This is used as a template for postitioning html elements and importing libraries/frameworks in all webpages in my web app. I used Django template "include" tags to include this in each template file I have for the site.
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

#### Navbar Template

Here I struggled to understand how to use template tags to set up links from the navbar to other pages in my app. After a good chunk of time, I figured it out with the help of the instructors and styled the navbar and footer. Then I used the "extends" template tag to allow the base.html page to inherit the footer and navbar. Since the base.html page is extended in each page of my site area, the navbar and footer is also in each one.

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

Here I wanted the links to span the entire height of the navbar and be aligned on the left of the screen. I also added hover effects. I hadn't used CSS in a while, so I took a bit of time to brush up on it and then got rolling here.
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

This was added to round out the site formatting.
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

#### Home Template

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

#### Home View Function

Then I added a function to the views for rendering the home page. After this, I registered my app's folder path and the home page to the website's urls.py file. 
```python
# Homepage
def home(request):
    # All we need is to render the template
    return render(request, 'FoodRecipeApp/FoodRecipeApp_home.html')
```

## Story 2 - Create Model, Model Form, Database, and Create Page

Here I set up the model functionality so that I could have the database items be rendered on to the user-facing template page in a form.

#### Model

For this I created the model and made the migration so that the database was set up.
```python
from django.db import models


MEALTYPE = [
    ("Appetizer", "Appetizer"),
    ("Entree", "Entree"),
    ("Side", "Side"),
    ("Beverage", "Beverage"),
    ("Dessert", "Dessert"),
]


# This is the model used for all saved data
class RecipeTracker(models.Model):
    title = models.CharField(max_length=60)
    mealType = models.CharField(max_length=60, choices=MEALTYPE)
    description = models.CharField(max_length=500)
    ingredients = models.CharField(max_length=700)
    nutritionTracked = models.CharField(max_length=500)

    def __str__(self):
        return self.title

    class Meta:
        verbose_name = "My Recipes"
        verbose_name_plural = "Recipe Info"

    objects = models.Manager()
```

#### Form Based on Model

This allows the form to be called with template tags to the html create page or edit page, respectively.
```python
from django import forms
from .models import RecipeTracker


# create a ModelForm
class RecipeForm(forms.ModelForm):
    # specify the name of model to use
    class Meta:
        model = RecipeTracker
        fields = "__all__"


# form to edit and individual recipe
class EditRecipeForm(forms.ModelForm):
    class Meta:
        model = RecipeTracker
        fields = {
            'title',
            'mealType',
            'description',
            'ingredients',
            'nutritionTracked',
        }
```

#### Make Create Template

This was fairly simple. I just had to debug how to get the form to render on the page as my only issue here.
```python
{% extends "FoodRecipeApp/FoodRecipeApp_base.html" %}
{% load static %}


<!-- This is a basic create recipe page -->
{% block content %}
<div class="jumbotron jumbotron-create-page">
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

#### Create View

Once I created this view, it was the perfect time to test out the database and the form to see if it could work. I encountered some errors as I ran through it so I worked on debugging those for a while. I fixed some syntax errors on the template page and a wrong character in the urls.py file for the whole site and then I was on my way.
```python
# Create page
def create(request):
    context = {}
    # create object of form
    form = RecipeForm(request.POST or None)
    # check if form data is valid
    if form.is_valid():
        # save the form data to model
        form.save()
        form = RecipeForm()
    context['form'] = form
    return render(request, 'FoodRecipeApp/FoodRecipeApp_create.html', context)
```

For my styling on the home page, I just aligned the text to the center. I went ahead to make sure it all worked and then boom, I was done with the story.


## Story 3 - Make Index Page

#### Index Template

Most of the difficulty here came from figuring out the template tags needed to loop through the model and bring each recipe in as a form. I also had to make sure the form labels and fields corresponded with each other properly. Once I figured that out and registered the url pattern, I let the bootstrap do the rest of the work for styling. Lastly, I added a view function to render the index page and made sure that the button on the navbar properly linked to the index page.

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

#### Index CSS

I keep this CSS very short, as I used bootstrap classes to good effect for styling.
```CSS
.manage-containers {
 opacity: .92;
 width: 55%;
 margin: auto;
}
```

#### Index View

Here I pass all the database objects through the context variable in the url. 
```python
def show_recipes(request):
    recipe = RecipeTracker.objects.all()
    context = {
        'recipe_list': recipe
    }
    return render(request, "FoodRecipeApp/FoodRecipeApp_showRecipes.html", context)
```

## Story 4 - Details Template

I started by creating this template here to received a single id of a database object and render that through this template. Then I registered the url pattern.

#### Details Template

This gets passed the ID through the url from the index template. You will also see the CSS in story 5 that applies in the same way to this template as it does to the edit template.
```python
{% extends 'FoodRecipeApp/FoodRecipeApp_base.html' %}
 
{% block content %}
  <!-- This is mostly bootstrap that shows a single recipes details. It is called from the showRecipes page -->
  <div class="manage-containers">
    <div class="list-group">
      <a href="#" class="list-group-item list-group-item-action flex-column align-items-start manage-containers-details">
        <div class="d-flex w-100 justify-content-between">
          <h5 class="mb-1">Recipe name: {{ recipe.title }}</h5>
          <small>Type of meal: {{ recipe.mealType }}</small>
        </div>
        <p class="mb-1">Description: {{ recipe.description }}</p>
        <p class="mb-1">Ingredients: {{ recipe.ingredients }}</p>
        <small>Nutrition: {{ recipe.nutritionTracked }}</small>
      </a>
    </div>
  </div>
  <!-- Button takes you to the editRecipe page -->
  <div class="button_container">
    <a href="{% url 'FReditRecipe' recipe.id %}"><button type="button" class="btn btn-primary button_align">Edit Recipe</button></a>
  </div>
{% endblock %}
```

#### Details View

Here I created the view and added a link in the index page in each image that calls this view and passes the ID. I had quite a bit of trouble figuring out how to get the exact id from the index page, so I spent quite a bit of time on that before solving it below.

```python
def recipe_details(request, pk):
    recipe = RecipeTracker.objects.get(pk=pk)
    context = {
        'recipe': recipe
    }
    return render(request, "FoodRecipeApp/FoodRecipeApp_recipeDetails.html", context)
```

## Story 5 - Edit and Delete Templates

After styling the create page earlier, I realized that I can reuse the code for the edit and delete pages as well, while keeping the style looking good. This adds to the efficiency of the program and is quicker to code as well.

#### Edit Template

This has the same formatting as the create page, but it adds a button that gives the option to delete a recipe. The only issue I ran into was getting the button to look good and stick just under the main form while being centered. I created this and registered the url as well. Once again the ID is passed through the url here.
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

#### Edit View

Here I had to pull the current object from the database, check for validity of the form submitted, and redirect as well. This took me quite a bit of time to finish.
```python
def edit_recipe(request, pk):
    recipe = get_object_or_404(RecipeTracker, pk=pk)
    if request.method == "POST":
        # instance is used to put the model data in the form as the page is rendered
        form = EditRecipeForm(request.POST, instance=recipe)
        if form.is_valid():
            recipe.save()
            return redirect('FReditRecipe', pk=recipe.pk)
    else:
        form = EditRecipeForm(instance=recipe)
    context = {
        'form': form,
        'pk': pk
    }
    return render(request, 'FoodRecipeApp/FoodRecipeApp_editRecipe.html', context)
```

#### Delete Template

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

#### Delete View

After finishing the edit view, this was pretty simple, since I mostly repeated steps I already had done.
```python
def delete_recipe(request, pk):
    recipe = get_object_or_404(RecipeTracker, pk=pk)
    if request.method == "POST":
        # confirming delete
        recipe.delete()
        return redirect('FRshowRecipes')
    context = {
        'recipe': recipe
    }
    return render(request, 'FoodRecipeApp/FoodRecipeApp_deleteRecipe.html', context)
```

#### CSS For Both Pages

This is intentionally very economical. I used very little CSS but still got the job done. The home page from earlier uses only the jumbotron crud form selector and a couple bootstrap classes, but the edit and delete pages also use the button container and button align css selectors, along with an additional bootstrap class.
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

Following the completion of these stories, I performed a very thorough testing of the entire app I created to make sure the functionality was as intended. I also cleaned up the comments and made sure that there wasn't any stray code lying around that was wasting space and time. And there it is! That is what I accomplished on my two-week sprint.
