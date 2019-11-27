

*** 1. execute ./prerequisites.sh

*** 2. Run the Database queries (Note: root user has no password, just enter.. :) )

    ** Start the database service
    sudo service mysql start
    ** Create database and database users

    sudo mysql -u root -p

    *mysql> CREATE DATABASE employee_db;
    *mysql> GRANT ALL ON *.* to db_user@'%' IDENTIFIED BY 'vagrant';
    *mysql> USE employee_db;
    *mysql> CREATE TABLE employees (name VARCHAR(20));

    ** Insert some test data
    *mysql> INSERT INTO employees VALUES ('PRATGYAN');

*** 3.  ./run.sh &
