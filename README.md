Step 1: Prepare the Server
2.Update your system to ensure all packages are up-to-date:
sudo apt update && sudo apt upgrade -y

Step 2: Install Required Software

2.1. Install Python 3.11
Ensure you have Python 3.11 installed, as the Dockerfile uses this version.
sudo apt install python3.11 python3.11-dev python3.11-venv -y

2.2. Install pip
Make sure that pip is installed to manage Python packages:
sudo apt install python3-pip -y

2.3. Install Poetry
Poetry is the package manager for Python dependencies.
curl -sSL https://install.python-poetry.org | python3 -
Poetry ko PATH mein add karna:
.bashrc file ko edit karen:
nano ~/.bashrc
File ke end mein yeh line add karen (agar already add nahi hai):
export PATH="$HOME/.local/bin:$PATH"

Changes ko apply karna:
Ab aapko .bashrc file mein ki gayi changes ko apply karne ke liye bash ko reload karna hoga:
source ~/.bashrc
After installation, verify the version of Poetry:
poetry --version
2.4. Install PostgresSQL
PostgreSQL is required for database management.
sudo apt install postgresql postgresql-contrib -y

After installation, start and enable PostgreSQL:
sudo systemctl start postgresql
sudo systemctl enable postgresql

You can check the status of PostgreSQL with:
sudo systemctl status postgresql

2.5. Install Redis
Redis will be used as the cache management middleware.
sudo apt install redis-server -y
Start and enable Redis:
sudo systemctl start redis
sudo systemctl enable redis
sudo systemctl status redis

Step 3: Set Up Your Application

3.1. Clone the Git Repository
Clone your repo from GitHub:
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
cd attendance-api

3.2. Install Application Dependencies
Use Poetry to install the necessary Python dependencies.
sudo apt install python3-poetry
poetry install
Screenshots
 ![image](https://github.com/user-attachments/assets/22ba1624-1cea-45f2-b142-ff77fa30f816)
 Update packages


Vi pyproject.toml
packages = [
    {include = "client"},
    {include = "models"},
    {include = "router"},
    {include = "utils"}
]
 ![image](https://github.com/user-attachments/assets/6ed74932-87e6-4c74-b6a9-309d30f4cc26)

 ## poetry install
![image](https://github.com/user-attachments/assets/8816c0ce-b72e-4466-a4a3-cfeb0cf227fb)
Failed because psycopg2 ko install karne ke liye libpq-dev package ki zaroorat hoti hai, jo ki PostgreSQL development headers aur libraries ko provide karta hai. Aap ye command run karein:

sudo apt update
sudo apt install libpq-dev

Ab poetry install command dobara run karein:

poetry install
![image](https://github.com/user-attachments/assets/0a6e3029-3560-4773-914d-56b2ac2f8122)
![image](https://github.com/user-attachments/assets/79632e57-8535-4b79-8fad-7cf59f02aef7)
Steps to Install Liquibase
Download Liquibase: Sabse pehle Liquibase ko download karna hoga. Ye command run karein:

sudo snap install liquibase

liquibase --version

make run-migrations
![image](https://github.com/user-attachments/assets/db22e7cc-da01-4b0b-a08e-4ffbd94c13f9)
Change run-migrations
![image](https://github.com/user-attachments/assets/0ce07e58-fb68-4300-9435-5a880c41563f)
13.232.188.111
wget https://jdbc.postgresql.org/download/postgresql-42.5.4.jar -P /home/ubuntu/attendance-api/liquibase_lib/



sudo vi /etc/postgresql/14/main/postgresql.conf
Uncomment listen_addresses
![image](https://github.com/user-attachments/assets/df905072-d3d5-47c8-8675-2976b850b341)
sudo vi /etc/postgresql/14/main/pg_hba.conf
![image](https://github.com/user-attachments/assets/6f10df28-4b4a-4566-8c89-9b873208efde)
![image](https://github.com/user-attachments/assets/5dc04ef0-d700-4af1-86e3-a1ad9076c645)
Add classpath
vi liquibase.properties 


classpath=/home/ubuntu/attendance-api/liquibase_lib/postgresql-42.5.4.jar
![image](https://github.com/user-attachments/assets/13bb4b18-2743-4a2f-9b66-b1982a33a990)
![image](https://github.com/user-attachments/assets/67fd11f6-6cda-4fcb-a53c-4f9f5d7fbab8)
![image](https://github.com/user-attachments/assets/de0a571b-863c-40bd-8397-260c5baab2c9)
sudo -u postgreS psql

ALTER USER postgres WITH PASSWORD password’ ;


sudo -u postgres psql
CREATE DATABASE attendance_db;
![image](https://github.com/user-attachments/assets/d6025ed1-601c-4afe-8ed5-bd84fb776ef0)
url=jdbc:postgresql://184.72.203.225:5432/attendance_db

http://3.84.20.150/
 liquibase --changeLogFile=db-changelog.xml update
![image](https://github.com/user-attachments/assets/a6ccd6cb-b383-48c0-8d84-3580174bf737)
Add  db-changelog.xml:

vi db-changelog.xml
![image](https://github.com/user-attachments/assets/6b5ddc2f-8168-4c8f-9caa-1d9b6d29efe5)
And run again 

liquibase --changeLogFile=db-changelog.xml update
![image](https://github.com/user-attachments/assets/bf80a643-762b-47cf-ad56-cc85c6425ee4)
liquibase --changeLogFile=migration/db-changelog.xml update
![image](https://github.com/user-attachments/assets/f74b53a0-8963-460d-a822-3455176608e0)
Now  

mv migration/db.changelog-master.xml migration/db-changelog.xml

And run again :
liquibase --changeLogFile=migration/db-changelog.xml update
![image](https://github.com/user-attachments/assets/d2935ee1-557a-4b0a-99eb-14dd5e0de8cb)
Run this command:

liquibase --changeLogFile=migration/db-changelog.xml --url=jdbc:postgresql://184.72.203.225:5432/attendance_db --username=postgres --password=password --driver=org.postgresql.Driver update
![image](https://github.com/user-attachments/assets/2000c0aa-d3c1-4598-9ed0-71ae49897656)
make run-migrations
![image](https://github.com/user-attachments/assets/f6546dd9-c302-4ca9-8fe2-3a3d3ee2211b)
 pip install python-json-logger

 pip install flask
![image](https://github.com/user-attachments/assets/4f800856-af2a-489c-9cef-da2fd002a0d0)
poetry add flasgger
pip install flasgger
![image](https://github.com/user-attachments/assets/57cd62c2-505f-45e3-86a6-d5e06cbc1866)
 poetry add prometheus_flask_exporter
 pip install prometheus_flask_exporter
![image](https://github.com/user-attachments/assets/57173677-2939-46e6-8ee4-c41ace593f09)
poetry add voluptuous
pip install voluptuous
![image](https://github.com/user-attachments/assets/9e5bcc94-4116-4f7a-91ec-87b8d91db1b1)
poetry add psycopg2
pip install psycopg2
![image](https://github.com/user-attachments/assets/aa5b9596-ebc6-4444-9d43-3c90a5a0f62e)
poetry add redis
pip install redis
![image](https://github.com/user-attachments/assets/c3d8db43-7d20-4da5-9ab4-04926e16e88b)
 poetry add flask-caching
 pip install flask-caching
![image](https://github.com/user-attachments/assets/191bdcd0-7a05-41de-b881-ac81959d6ee0)
poetry add peewee
pip install peewee
![image](https://github.com/user-attachments/assets/3847cdd3-eb81-42e3-9b85-e3a0d5f9c6a7)

