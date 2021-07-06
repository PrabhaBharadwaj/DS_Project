# ML-Model-Flask-Heroku-Deployment  and Deployed in AWS EC2 
ML Model Flask Heroku deployment sample and same deployed in AWS EC2 instance also


# Salary_Prediction

This is a demo project to elaborate how Machine Learn Models are deployed on production using Flask API.

## Prerequisites
You must have Scikit Learn, Pandas (for Machine Leraning Model) and Flask (for API) installed.

## Project Structure
This project has four major parts :

##### 1. model.py - This contains code fot our Machine Learning model to predict employee salaries absed on trainign data in 'hiring.csv' file.
##### 2. app.py - This contains Flask APIs that receives employee details through GUI or API calls, computes the precited value based on our model and returns it.
##### 3. request.py - This uses requests module to call APIs already defined in app.py and dispalys the returned value.
##### 4. templates - This folder contains the HTML template to allow user to enter employee detail and displays the predicted employee salary.

## Running the project
1. Ensure that you are in the project home directory. Create the machine learning model by running below command -
python model.py
This would create a serialized version of our model into a file model.pkl

2. Run app.py using below command to start Flask API
python app.py
By default, flask will run on port 5000.

3. Navigate to URL http://localhost:5000
You should be able to view the homepage as below : alt text

4. Enter valid numerical values in all 3 input boxes and hit Predict.

If everything goes well, you should be able to see the predcited car price vaule on the HTML page! alt text

You can also send direct POST requests to FLask API using Python's inbuilt request module Run the beow command to send the request with some pre-popuated values -
python request.py

# Deployed in Heroku

Here we used Flask web application Framework and deployed in Heroku  (Platfoem As A service-IAAS) 

*************************** HERUKU **************************

Cloudaplication Platform
Heroku is a container-based cloud Platform as a Service (PaaS). Developers use Heroku to deploy, manage, and scale modern apps. 
Our platform is elegant, flexible, and easy to use, offering developers the simplest path to getting their apps to market.

1) Before deploy clone all our code project folder in github
2) Keep local project folder same name as repository name and upload all file to repository
3) Heruku platform to deploy our code by creating new app(Providing app name)
4) In deploy section "Deployment method" as Github, Provide our github repository name and Repo name: Give our github carprediction folder name by searching there

5) After connecting reponame, just "deploy Branch" option.
5) Build master tab will show the deployment process and shows green tick mark to below items
	Receive code from GitHub
	Build master 90c790d3
	Release phase
	Deploy to Heroku
	Your app was successfully deployed.

6) After deployement click on view or open app, we can get the web page we built for prediction.


# Deployed in AWS EC2

High level steps:
	1) Flask Code
	2) Run and Check in Local
	3) Create AWS account
	4) Create EC2 Instance
	5) Download Putty and putty gen, Winscp
	6) Generate Private with help of puttygen
	7) Update the port in Flask app.py
	8) Install the libraries by connecting through Putty
	9) Run python3 app.py in putty
	10. Execution URL/Web url from EC2 instance and verify it.
	11) Disable Instance

### Deployment main files FOR AWS EC2:
		app.py
		MLDemoTesting.pem (This req to generate .ppk file)
		MLDemoTesting.ppk
		model.pkl
		procfile
		requirements.txt
		templates folder with home.html
		static folder with css folder with style file (Depends)
    
Here we used Flask web application Framework and deployed in Amazon (AWS) EC2 platform (Infrastructure As A service-IAAS) 

1) Login to AWS --> Search EC2 (Its a virtual server in cloude)--> Running Instance --> Launch Instance

2) Create AWS EC2 Instance:
  Now we are creating a cloud server, here we deploy our model and create api outof it
	Here we have many free tier server to create in cloud 

	--> Search Ubantu free tier and select(Any freeone can select) --> t2.micro (Free tier eligible) --> Review and Launch  --> Launch

	--> Select New key pair (Keypair pop up comes) (Whenever new instance create new keypair) --> Type 'MLDemoTest' (Key pair name) --> Press Download keypair

	--> Copy that downloaded file (MLDemoTesting.pem) in our project file(This helps us tocreate the private key via puttygen, this private key help us to interact with Linux env)
	
	--> Launch Instance(We can type any name (TestPrabha) while its lauching)

3) Make this instances accessable from everywhere. Make this setting in EC2
	Select the instance and then in leftside list
		--> Networks & Security --> Security Group --> Create a Security Group
			--> Security Groupname as "FullAccess" 
			--> Description as "FullAccess" 
		--> Click add rule
		In "INBOUND"
		--> Type as "All Traffic " (This is the various protocal to communicate with this api)
		--> Source as "Anywhere"
	--> Now select Create

4) Now we need to link this security group to EC2:
	Goto --> Networks & Security --> Networks Interfaces --> Right click on 1st interface id --> Select "Change security group"
		--> In Associated security groups selct "FullAccess" Named newly created security Group --> Save
		--> Now we can see security groups as "FullAccess" 


5) In Puttygen: To create Private Key using pem file
	--> Convert .ppk version 3 to 2 , else it will fail later(One time)
		Inside Puttygen --> Key -->Parameter for saving Keys  -->vesrion change 3 to 2
		
	--> Select Load --> Load our MLDemoTesting.pem file  --> Open 
		--> OK(Successfull imported privatekey ) --> Save Private Key --> Without Pharser
		--> Give name as 'MLDemoTesting' and provide our location--> It saves from pem file as .ppk fileSave Private key in .ppk  (This is a privatekey)

6) In EC2 Copy the Public DNS:
	--> Now goto EC2 instance newly created(Testprabha) instance --> ActionS --> Connect  ( to your instance, there we will get out winscp required hostname. Which is Public DNS)
		--> In 'SSH Client' tab copy Hostname / (Connect to your instance using its Public DNS:) ec2-13-229-242-115.ap-southeast-1.compute.amazonaws.com

7) Connect to EC2 via Winscp:
	--> Winscp helps to deploy code in EC2 instance just like connecting to server and drag and drop

	-->Inside Winscp Copy above Public DNS as Hostname here -->Username Default as 'ubuntu' --> in  Advanced select Authentication-->
		--> selct the uploading option to selct private key file "MLDemoTesting.ppk" file(this is a private key to connect with ubuntu ec2 server)
		--> Ok -->Login -->yes
  		--> Now it coonects to AWS EC2 and shows empty folder in winscp (/home/ubuntu)


	--> Now drag drop all our code from local to winscp AWS ec2 folder
		app.py  
		model.pkl  
		requirements.txt  
		folder: templates

8) Connect to EC2 via putty:
	--> Copy above Public DNS as Hostname here --> Type "MLDemoTest" as saved session and save
	--> Goto SSH -->Goto Auth --> Privatekeyfor authantication select "MLDemoTest.ppk" ---> Press Open
	--> Now putty Command Prompt opens --> Type 'ubuntu' as login as
	--> Now it connects to EC2 server : ubuntu@ip-172-31-45-206:~$
	--> Type pwd shows our directory (/home/ubuntu)

9) We need to install few libraries in ec2, so we connected to putty command prompt (All the library available in requirement.txt , we need to install)

	pip3 install panda   
		--> This shows error, so type below lines (coz version are not sync)
	sudo apt-get update && sudo apt-get install python3-pip

	#This to install all libraries in req.txt file in unbuntu ec2 
	pip3 install -r requirements.txt

10) Deploy now in putty
	Write below command in putty 
		python3 app.py

	Now it will execute in 8080 portal and show message " Running on http://0.0.0.0:8080/ (Press CTRL+C to quit)"

11) EC2 Deployed and checking via URL
	In our instance Status check shows as passed
	select our instance -->Connect --> There we will get our URL(Public DNS)  ec2-13-229-242-115.ap-southeast-1.compute.amazonaws.com
	
	URL:
		Copy this in google and write :8080 at the end
		 ec2-13-229-242-115.ap-southeast-1.compute.amazonaws.com:8080

