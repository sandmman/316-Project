##Run and Setup on Duke VM w/Vagrant##

### Required Packages ###
- django-tables2 --> from vm run `sudo pip install django-tables2`
- django_chartit --> from vm run `sudo pip install django_chartit`
  - Also have to edit /chartit/templatetags/chartit.py

    ```
    -from django.utils import simplejson
    +import simplejson
    ```

  - Also we have to make these changes, in order to handle datetime types for the charts
    `https://github.com/bastir85/django-chartit/commit/aa47dc1d5f7e13e72c0f96fa22e61788b89afc4b`

### Setup ###
1. Run vagrant up then ssh into the vm in your terminal
2. Navigate into `/316-Project/running_log/`
3. If you haven't, you must initiate the database by running
  - `dropdb log; createdb log;`
4. Update and migrate the app files
  - `python manage.py makemigrations log`
  - `python manage.py migrate`
5. Run the local host server of your VM
  - `python manage.py runserver`
  - Then, create a user so the data loaded in the next step is accepted.
  - port 8000 is the default, so if you open the VirtualBox VM you should just have to go to localhost:8000 on a web browser
  - Stop running the server (control+C)
6. Initialize date for database
  - `python manage.py loaddata users`
  - `python manage.py loaddata activities`
    - Contains 300 entries for user with id = 1 and 2000 entires for the other users.
7. Run the local host server of your VM
  - `python manage.py runserver`
