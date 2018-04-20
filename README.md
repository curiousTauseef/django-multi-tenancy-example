# Multi-tenancy Django Example

Example of multi-tenancy using Django 1.11 and MySql.

## Step by Step to Install:

First of all, have pip and virtualenv installed.

1. Create a virtualenv for the project by prescribing Python 3:<br>
```virtualenv --python = python3 [environment name]```

2. Enter the virtualenv folder and activate it:<br>
```source bin/activate```

3. To install the ```mysqlclient``` driver make sure you have installed the dependencies below: <br>
```sudo apt-get install python-dev python3-dev``` <br>
```sudo apt-get install libmysqlclient-dev```

4. Install the required packages: <br>
```pip install -r requirements.txt```<br>
(NOTE) some bugs were found in the ```django-db-multitenant==0.3.2``` library. So a fork was created with the problem already fixed (https://github.com/diegofsousa/django-db-multitenant). The above command already installs the version with bugs fixed.

5. Create the databases in <i>mysql command line</i>. In the following example we will use two tenants (```tenant1``` and ```tenant2```), however you can change it with whatever you want. NOTE: Each database will be a tenant. Here is an example of how it should be created: <br>
```CREATE DATABASE tenant1 CHARACTER SET utf8;``` <br>
```CREATE DATABASE tenant2 CHARACTER SET utf8;``` 

6. Make the database settings in ```settings.py``` as follows:<br>
``` 
DATABASES = {
    'default': {
        'ENGINE': 'db_multitenant.db.backends.mysql',
        'NAME': 'tenant',
        'USER': 'YOUR DATABASE USERNAME',
        'PASSWORD': 'YOUR DATABASE PASSWORD',
        'HOST': 'localhost',
        'PORT': 'YOUR DATABASE PORT',
    }
} 
```

One of the tenants will be used in this configuation only for Django not to complain about syntax error.

7. Add the hosts file (in Linux OS: ```/etc/hosts/```) for your computer, pointing to ```127.0.0.1``` as the tenants were created:<br>
``` 
127.0.0.1       tenant1.example
127.0.0.1       tenant2.example
```

6. Migrate the databases:<br>
```TENANT_DATABASE_NAME=tenant1 ./manage.py migrate``` <br>
```TENANT_DATABASE_NAME=tenant2 ./manage.py migrate```

7. Enter the "app" folder and install pip dependencies:<br>
```pip install -r requirements.txt```

8. Run your application with ```./manage.py runserver``` and access your tenants with: <br>
```http://tenant1.example:8000``` for <b>tenant1</b> and ```http://tenant2.example:8000``` for <b>tenant2</b>.

## Credits
<ul>
  <li>Diego Fernando and Renan Xavier.</li>
</ul>
