### Full Stack API Final Project
## Project Description
Trivia app is a web application that allows people to play trivia questions from various fields of life. 
The application does the following:

Display all available questions and question groups based on categories. Each question displays the question, category adn difficulty rating by default. It also shows the answer whose visibility can be toggled, on or off.
Delete questions.
Add questions and require that they include question and answer text.
Search for questions based on a text query string.
Play the quiz game, randomizing either all questions or within a specific category.
Follow the instructions below to get started! Also check out my blog to see my reflection and takeaways from compeleting this project!

## Getting Started
Installing Dependencies
Python 3.7
Follow instructions to install the latest version of python for your platform in the python docs

## Virtual Enviornment
We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the python docs

PIP Dependencies
Once you have your virtual environment setup and running, install dependencies by naviging to the /backend directory and running:

pip install -r requirements.txt
This will install all of the required packages we selected within the requirements.txt file.

## Key Dependencies
Flask is a lightweight backend microservices framework. Flask is required to handle requests and responses.

SQLAlchemy is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in init.py and can reference models.py.

Flask-CORS is the extension we'll use to handle cross origin requests from our frontend server.

### Installing frontend dependencies
This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the frontend directory of this repository. After cloning, open your terminal and run:

npm install

This will install all the front end dependencies from package.json

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
psql -f trivia.psql -U your_database_username -d database_name

# Running the server
From within the backend directory first ensure you are working using your created virtual environment.

To run the server, execute:

  $ export FLASK_APP=flaskr
  $ export FLASK_ENV=development
  $ flask run

Running Your Frontend in development Mode

The frontend app was built using create-react-app. In order to run the app use npm start. You can change the script in the package.json file.

Open http://localhost:3000 to view it in the browser. The page will reload if you make edits.

npm start


# Testing
To run the tests for all endpoints do the following

DROP DATABASE trivia_test
CREATE DATABASE trivia_test

from your terminal:
psql -f trivia.psql -U your_database_username -d database_name

run python test_flaskr.py to check the tests

## API Reference

Getting Started
Backend Base URL: http://127.0.0.1:5000/
Frontend Base URL: http://127.0.0.1:3000/
Error Handling
Errors are returned in the following json format:

```json 
{
    "success": False,
    "error": 404,
    "message": "Resource not found"
}
```
This API returns 3 types of errors:

400: bad request
404: not found
422: Unprocessable

Endpoints
GET '/categories'
returns a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category

Example: curl http://127.0.0.1:5000/categories
```json
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "success": true
}
GET '/questions'
returns all the questions in the database and a category dictionary. The questions are paginated with 10 questions each page.
Example: curl http://127.0.0.1:5000/questions
{
  "categories": {
    "1": "Science", 
    "2": "Art", 
    "3": "Geography", 
    "4": "History", 
    "5": "Entertainment", 
    "6": "Sports"
  }, 
  "questions": [
    {
      "answer": "Apollo 13", 
      "category": 5, 
      "difficulty": 4, 
      "id": 2, 
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    }, 
    {
      "answer": "Maya Angelou", 
      "category": 4, 
      "difficulty": 2, 
      "id": 5, 
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    }, 
    {
      "answer": "Edward Scissorhands", 
      "category": 5, 
      "difficulty": 3, 
      "id": 6, 
      "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
    }, 
    {
      "answer": "Muhammad Ali", 
      "category": 4, 
      "difficulty": 1, 
      "id": 9, 
      "question": "What boxer's original name is Cassius Clay?"
    }, 
    {
      "answer": "Brazil", 
      "category": 6, 
      "difficulty": 3, 
      "id": 10, 
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    }, 
    {
      "answer": "Uruguay", 
      "category": 6, 
      "difficulty": 4, 
      "id": 11, 
      "question": "Which country won the first ever soccer World Cup in 1930?"
    }, 
    {
      "answer": "George Washington Carver", 
      "category": 4, 
      "difficulty": 2, 
      "id": 12, 
      "question": "Who invented Peanut Butter?"
    }, 
    {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "The Palace of Versailles", 
      "category": 3, 
      "difficulty": 3, 
      "id": 14, 
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }
  ], 
  "success": true, 
  "total_questions": 18
}
DELETE '/questions/int:id'
Delete questions by id specified in the url parameter.
Example: curl -X DELETE http://127.0.0.1:5000/questions/12
{
    "success": "True",
    "deleted": 12
}

## POST '/questions'

Creates a new question and adds it to the database. The new question must have all four information, which are, 
Question, Answer, Category, Difficulty

Example: curl -X POST - H "Content-Type: application/json" -d '{"question": "Who won the 2021/2022 English Premier League?", "answer": "Manchester City", "difficulty": 1, "category": "6"}' http://127.0.0.1:5000/questions

{
  "success": true
  "created": 18
  "total_questions": 18
}

The search feature is implemented within the endpoint for creating new questions using an if check.
POST '/questions'
User type in a string to search for a question and it will return all the questions that contain this string.
Example: curl -X POST -H "Content-Type: application/json" -d '{"searchTerm": "Abstract Expressionism"}' http://127.0.0.1:5000/questions
it returns:
{
  "questions": [
    {
      "answer": "Jackson Pollock", 
      "category": 2, 
      "difficulty": 2, 
      "id": 19, 
      "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
    }
  ], 
  "success": true, 
  "total_questions": 1
}

GET '/categories/int:id/questions'
Get questions based on a category.

Example: curl http://127.0.0.1:5000/categories/3/questions
{
  "questions": [
     {
      "answer": "Lake Victoria", 
      "category": 3, 
      "difficulty": 2, 
      "id": 13, 
      "question": "What is the largest lake in Africa?"
    }, 
    {
      "answer": "The Palace of Versailles", 
      "category": 3, 
      "difficulty": 3, 
      "id": 14, 
      "question": "In which royal palace would you find the Hall of Mirrors?"
    }, 
    {
      "answer": "Agra", 
      "category": 3, 
      "difficulty": 2, 
      "id": 15, 
      "question": "The Taj Mahal is located in which Indian city?"
    }
  ], 
  "success": true, 
  "total_questions": 3
}
POST '/quizzes'
Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
Example: curl -X POST -H "Content-Type: application/json" -d '{"previous_questions": [2, 6], "quiz_category": {"type": "Sports", "id": "11"}}' http://127.0.0.1:5000/quizzes
{
  "question": {
      "answer": "Uruguay", 
      "category": 6, 
      "difficulty": 4, 
      "id": 11, 
      "question": "Which country won the first ever soccer World Cup in 1930?"
    }, 
  "success": true
}
```