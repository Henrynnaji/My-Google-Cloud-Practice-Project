# LAB: Essential Google Cloud Infrastructure: Foundation
	Creating Virtual Machines
	
##Objectives:

In this lab, you explore the available options for VMs and see the differences between locations.

In this lab, you learn how to perform the following tasks:

	-Create several standard VMs

	-Create advanced VMs
	
	
##Steps:

1. Create a utility virtual machine 

gcloud compute intsance create henry-vm1 
		--machine-type 'n1-standard-1' 
		--zone 'us-central1-c'  
		--image-project 'debian-cloud' 
		--image 'debian-10-buster-v20200910' 
		--subnet 'default'

2. Create a Windows virtual machine
gcloud compute instances create windows-vm 
		--zone 'europe-west2-a' 
		--machine-type 'n1-standard-2' 
		--subnet 'default' 
		--tags 'http-server,https-server' 
		--image 'windows-server-2016-dc-core-v20200908' 
		--image-project 'windows-cloud 
		--boot-disk-size '100GB' 
		--boot-disk-type 'pd-ssd' 
		--boot-disk-device-name 'windows-vm'
		
###Allow HTTP traffic
gcloud compute firewall-rules create default-allow-http 
		--direction 'INGRESS'
		--network 'default'
		--action 'ALLOW' 
		--rules 'tcp:80' 
		--source-ranges '0.0.0.0/0' 
		--target-tags 'http-server'
		
###Allow HTTPS traffic
gcloud compute firewall-rules create default-allow-https --direction 'INGRESS' --network 'default' --action 'ALLOW' --rules 'tcp:443' --source-ranges '0.0.0.0/0' --target-tags 'https-server'
		

3. Create a custom virtual machine
gcloud compute instances create custom-vm1 
		--zone 'us-west1-b' 
		--machine-type 'n1-standard-2' 
		--subnet 'default' 
		--tags 'http-server,https-server' 
		--image 'windows-server-2016-dc-core-v20200908' 
		--image-project 'windows-cloud 
		--boot-disk-size '32GB'  
		--boot-disk-device-name 'custom-vm1'
		
###Connet via SSH to your custom VM
	
		- to connect to custom-vm1:
		
				gcloud compute ssh custom-vm1
		
		-To see information about unused and used memory and swap space on your custom VM, run the following command:
		
				free
				
		-To see details about the RAM installed on your VM, run the following command:
				
				sudo dmidecode -t 17
				
		-To verify the number of processors, run the following command:
				
				nproc
				
		-To see details about the CPUs installed on your VM, run the following command:
			
				lscpu
				
				
				
				
				
				
				
				
				
				
				
				
				
				
# LAB: Google Cloud Fundamentals: Getting Started with App Engine


##Objectives
In this lab, you learn how to perform the following tasks:

Initialize App Engine.

		- Preview an App Engine application running locally in Cloud Shell.

		- Deploy an App Engine application, so that others can reach it.

		- Disable an App Engine application, when you no longer want it to be visible.
		
		
##Steps:


### Activating Google cloud shell.

		- how to activate google cloud shell:
			
			gcloud cloud-shell
			
		- You can list the active account name with this command:
			
			gcloud auth list
		
		-You can list the project ID with this command:
		
			gcloud config list project



2. Initialize App Engine

		- Initialize your App Engine app with your project and choose its region:
			
			gcloud app create --project=$DEVSHELL_PROJECT_ID
			
			
		- Clone the source code repository for a sample application in the hello_world directory:
		
			git clone https://github.com/GoogleCloudPlatform/python-docs-samples
			
			
		- Navigate to the source directory:
		
			cd python-docs-samples/appengine/standard_python3/hello_world
			
			
			
3. Run Hello World application locally

		- Execute the following command to download and update the packages list.
				
				sudo apt-get update
				
		- Set up a virtual environment in which you will run your application. Python virtual environments are used to isolate package installations from the system
		
				sudo apt-get install virtualenv
				
				Note: If prompted [Y/n], press Y and then Enter.
				
				virtualenv -p python3 venv
		
		- Activate the virtual environment.
		
				source venv/bin/activate
				
		
		- Navigate to your project directory and install dependencies.
		
				pip install  -r requirements.txt
				
				
		- Run the application:
				
				python main.py
