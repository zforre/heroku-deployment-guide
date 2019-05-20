## Heroku Deployment

1. Update Pipfile.lock

* ONLY DO THIS IF THE PYTHON VERSION YOU'RE USING IS NOT SPECIFIED
* specify python version in your Pipfile, e.g. python_version = '3.7'
* $ pipenv lock

2. Create a Procfile

3. Install gunicorn

* gunicorn is a production suitable web server
* $ pipenv install gunicorn==19.9.0
* update your Procfile
	* web: gunicorn <project_name>.wsgi --log-file -
	* <project_name> should be the name of your project, e.g. conf
	* server configuration is contained in the wsgi.py file

4. Install whitenoise

	* $ pipenv install whitenoise==3.3.1
	* update settings.py
		* add 'whitenoise.runserver_nostatic' above 'django.contrib.staticfiles' in INSTALLED_APPS
		* add 'whitenoise.middleware.WhiteNoiseMiddleware' to MIDDLEWARE directly after the Django SecurityMiddleware

5. Add STATIC_ROOT and STATICFILES_STORAGE at the bottom of your settings.py file

	* STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
	* STATICFILES_STORAGE = 'whitenoise.storage.CompressedManifestStaticFilesStorage'

6. Create Heroku app

7. Add Heroku URL to settings.py file

	* Add the Heorku domain to the ALLOWED_HOSTS list in settings.py
	* Copy and paste everything except the https://
