Microsoft SQL Server ODBC Driver 1.0 for Ubuntu 14.04 
=====================================================

Check out excellent article: http://onefinepub.com/2013/03/ms-sql-odbc-ubuntu/

##Install script tested on ubuntu 14.04

```sh
#!/usr/bin/env bash
#http://onefinepub.com/2013/03/ms-sql-odbc-ubuntu/

cd
wget https://raw.githubusercontent.com/tax/mssqldriver/master/unixodbc_2.3.2-1_amd64.deb
sudo dpkg -i unixodbc_2.3.2-1_amd64.deb

wget https://raw.githubusercontent.com/tax/mssqldriver/master/msodbcsql-11.0.2270.0.tar.gz
tar xf msodbcsql-11.0.2270.0.tar.gz 
cd msodbcsql-11.0.2270.0
rm install.sh build_dm.sh
wget https://raw.githubusercontent.com/tax/mssqldriver/master/install.sh
wget https://raw.githubusercontent.com/tax/mssqldriver/master/build_dm.sh
bash install.sh install --accept-license --force

ln -s /lib/x86_64-linux-gnu/libcrypto.so.1.0.0 /usr/lib/x86_64-linux-gnu/libcrypto.so.10;
ln -s /lib/x86_64-linux-gnu/libssl.so.1.0.0 /usr/lib/x86_64-linux-gnu/libssl.so.10;
ln -s /usr/lib/x86_64-linux-gnu/libodbcinst.so.2.0.0 /usr/lib/x86_64-linux-gnu/libodbcinst.so.1;
ln -s /usr/lib/x86_64-linux-gnu/libodbc.so.2.0.0 /usr/lib/x86_64-linux-gnu/libodbc.so.1

# Cleanup
cd 
rm -R msodbcsql-11.0.2270.0
rm msodbcsql-11.0.2270.0.tar.gz
rm unixodbc_2.3.2-1_amd64.deb

```

Example django settings for django using https://github.com/lionheart/django-pyodbc

```python
# Example django settings

DATABASES = {
    'default': {
        'ENGINE': "django_pyodbc",
        'HOST': 'tcp:xxxxxx.database.windows.net,1433',
        'USER': 'testuser@xxxxxx',
        'PASSWORD': "SecretP#SS",
        'NAME': 'djangotest',
        'OPTIONS': {
            'host_is_server': False,
            'autocommit': True,
            'driver': "ODBC Driver 11 for SQL Server"
        },
    }
}

```