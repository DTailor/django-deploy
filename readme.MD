Django + uWSGI + Supervisord
=======
    If you're the first one to init an app instance with supervisord + uwsgi,
    continue, else skip step 1.
    1. Prepare the ground.
        1. Install supervisor
            > sudo pip install supervisor
        2. Install uwsgi. Version should be >=2
            > sudo apt-get install uwsgi
        3. Enter root mode
            > sudo su
        4. Create sample config file for supervisord
            > echo_supervisord_conf > /etc/supervisord.conf
            > supervisord -c /etc/supervisord.conf
        5. Edit the config file by appending these 2 lines
            [include]
            files = supervisord/conf.d/*.conf
        6. Create project config folder for supervisord
            > mkdir /etc/supervisord
            > mkdit /etc/supervisord/conf.d
    2. Create the uwsgi config file in ~/project_root/docs or any other prefered directory from the example provided in configs/app-uwsgi.ini
    3. Config the app with supervisord.
        1. Create sample config file for the project
            > touch /etc/supervisord/conf.d/project-name.conf
        2. Append the sample supervisord data from config/app-supervisord.conf
        3. Make supervisord find new config files without touch already running instances
            > supervisorctl update
            > supervisorctl start app



Supervisor commands:
====
    1. supervisorctl status - show current status of all processes
    2. supervisorctl start|stop|restart <_proc1> <_proc2> ... - does the following action to a single or list of processes
    3. supervisorctl reload - restarts all application including new ones
    4. supervisorctl update - restart the applications which config files were changed, new ones will not start.