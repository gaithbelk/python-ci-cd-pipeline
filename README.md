# projet-devops


## this is a flask application deployed on a heroku server

## steps
- create github project
- clone it to my pc
- create a new python virtual environment and activate it
- Install flask and pytest in myvenv (pip install flask pytest)
- pip freeze > requirements.txt
- create src folder and app.py
- create tests folder and test_app.py
- export PYTHONPATH=src
- pytest =>  our test is run successfully
- push first commit


## Continuous integration :
- Go to Actions in github and press Create and test a Python application.
- adding pytest and exporting PYTHONPATH=src in workflow yml file
- A bunch of indentation errors :(
- and workflow working successfully

## Continuous deployment :
- installing heroku cli
- heroko create and now we have our default template deployed on https://blooming-reaches-72689.herokuapp.com/
- git push heroku main : our flask app will be running on this server with this url
- but we don't want to do this manually everytime we change something  we want this to run automatically therefore we will make a new github action that will deploy our code
- heroku authorizations:create to create a token => we have our token now
- then we add it as a secret in github called HEROKU_API_KEY
- then we add HEROKU_APP_NAME as a secret to ( which value is blooming-reaches-72689 )

- adding this code to github python-app.yml file 
      env:
        HEROKU_API_TOKEN: ${{ secrets.HEROKU_API_TOKEN }}
        HEROKU_APP_NAME: ${{ secrets.HEROKU_APP_NAME }}
      if: github.ref == 'refs/heads/master' && job.status == 'success'
      run: |
        git remote add heroku https://heroku:$HEROKU_API_TOKEN@git.heroku.com/$HEROKU_APP_NAME.git
        git push heroku HEAD:main -f 

- adding Procfile (used to deploy any type of application on heroku)

# 3 hours later

It's finally deployed and 100% working, if I change anything in the app.py, commit then push changes the python-app.yml file will be executed again
and changes will appear in the website.
You can check it here.

https://blooming-reaches-72689.herokuapp.com/
