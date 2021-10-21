# FormShare Stack
[Pyramid]( https://trypyramid.com/) is a great framework for developing web applications that also supports the development of ["Extensible" and "Pluggable"]( http://docs.pylonsproject.org/projects/pyramid/en/latest/narr/extending.html) software based on certain rules. However, there is no much documentation on how to create such type of applications.

[CKAN]( https://ckan.org/) is an excellent example of a Web application that can be extended or customized using plug-ins. It relies on [PyUtilib Component Architecture]( https://pypi.python.org/pypi/PyUtilib) (PCA) to declare a series of interfaces and extension points that then are used by plug-ins to hook in. It also implements a series of [Jinja2]( http://jinja.pocoo.org/) extension (notably CKAN_EXTENDS) that allows easily template inheritance between CKAN and connected plug-ins.

During the development of  [FormShare](https://github.com/qlands/FormShare)  we borrowed certain concepts and code from CKAN to create a series of technologies to make FormShare a extensible and pluggable Web Application. These technologies are now stacked in FormShare Stack (FStack).

FStack is a CookieCutter template to create scaffolding for scalable and pluggable Web Applications. It can can be used as a starting point to develop more complex Web Applications. The resulting project will have:

- Easy JS and CSS resource declaration and injection using Jinja2 Tags
- Database migrations using Alembic
- PCA extensibility
  - Adding new routes
   - Adding and overwriting templates
   - Adding and injecting new static resources
   - Adding and injecting new JS or CSS resources
 - [AdminLTE](https://adminlte.io) (3.0.5) HTML template system
 - User registration and login using MySQL

## Requirements

FormShare stack depends on MySQL, Redis and Python

```sh
# On Ubuntu 20.04
sudo apt-get install -y redis-server mysql-server python3.8-venv
```

## How to create a FStack project

```shell
python3 -m venv myproject_env
. ./myproject_env/bin/activate
pip install cookiecutter
cookiecutter https://github.com/qlands/fstack
```

## Notes

- The FStack CookieCutter assumes that your MySQL server root account has a password. If your account does not have a password then edit the config.ini file to remove the colons (:) between the user the password. The same for alembic.ini and run again "alembic upgrade head"

  ```ini
  sqlalchemy.url = mysql+mysqlconnector://root@localhost/test_project?charset=utf8&ssl_disabled=True
  ```

- In some Linux distributions MySQL cannot connect to localhost but to 127.0.0.1. If you get a connexion refused edit the config.ini file to change localhost to 127.0.0.1. The same for alembic.ini and run again "alembic upgrade head"

  ```ini
  sqlalchemy.url = mysql+mysqlconnector://root@127.0.0.1/test_project?charset=utf8&ssl_disabled=True
  ```

  
