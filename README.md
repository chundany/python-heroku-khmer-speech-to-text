# Python Khmer Speech to Text API

A Django app (deployed on Heroku) for creating and handling long running asynchronous requests to Google Speech API. For instructions and more information, see the [firebase frontend repo](https://github.com/RyanQuey/khmer_speech_to_text).

## Uploads and Transcription Dashboard
We track and display progress as the file uploads to Google Storage, as it is transcribed to Google Speech API, and as it is returned and stored by Firebase.

![Uploading audio](https://github.com/RyanQuey/python-heroku-khmer-speech-to-text/raw/master/screenshots/uploading-audio-file.png)

## Transcript Results
Transcript includes highlights based on accuracy percentage, and lists possible alternatives on hover. Metadata about the file and the transcription is persisted for future reference.

![Transcript Result](https://github.com/RyanQuey/python-heroku-khmer-speech-to-text/raw/master/screenshots/transcript-result.png)

## Running Locally

Make sure you have Python 3.7 [installed locally](http://install.python-guide.org). 

```sh
# clone the repository
git clone https://github.com/RyanQuey/python-heroku-khmer-speech-to-text.git
cd python-heroku-khmer-speech-to-text

# install venv if don't have it already
sudo apt-get -y install python3-venv

# open the virtual env in current project
python3 -m venv venv

# If need to get pip (which, there's a decent chance you won't), can run: 
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py

# install project dependencies
python3 -m pip install -r requirements.txt

# If got following error, will need to install some stuff:
# `You need to install postgresql-server-dev-X.Y for building a server-side extension or libpq-dev for building a client-side application`
# See here: https://stackoverflow.com/a/28938258/6952495
# If you did, will need the following dependencies in order to install django. If so run the following:
sudo apt-get install python-psycopg2
sudo apt-get install libpq-dev

# Now need to set some env vars
cp ./.env.sample ./.env

# You're going to want to go in there and change those env vars to fit your setup

# start local server
heroku local

# OR alternatively, can use Honcho for some extra features
python3 -m pip install honcho
honcho start -f Procfile.dev
```

Your app should now be running on [localhost:5000](http://localhost:5000/).

We don't have any actual views, but you can still go there to see if the app is running. 

Now your frontend can hit this python api server.

## Opening a Console
### If using honcho, can open a console

```sh
python3 -m pip install honcho
honcho run python
```

## Deploying to Heroku
To push to Heroku, you'll need to install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-cli).

```sh
heroku create
git push heroku master

# If had a db:
# heroku run python manage.py migrate

heroku open
```

# Released under MIT License

Copyright (c) 2020 Ryan Quey.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
