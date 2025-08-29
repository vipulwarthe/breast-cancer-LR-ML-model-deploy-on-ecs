
## Deployment

To deploy this project create one ubuntu 20.04 ec2 t2.medium/all traffic-sg and 30gb storage instance and connect with vscode and run below commands:

```
sudo apt update && sudo apt upgrade -y
```
```
if you want to run notebook locally use below command to activate conda env in local system and run notebook

wget https://repo.anaconda.com/miniconda/Miniconda3-py38_23.3.1-0-Linux-x86_64.sh
```
```
bash Miniconda3-py38_23.3.1-0-Linux-x86_64.sh
```
```
source ~/.bashrc
```
```
conda create -n Health python=3.11 ipykernel
```
```
conda activate Health
```
```
python -m ipykernel install --user --name=student
```
```
git clone https://github.com/vipulwarthe/deploy-ml-model-on-ecs.git
```
```
cd deploy-ml-model-on-ecs            (give the permission 777 to this folder)
```
```
pip install -r requirements.txt
```
```
pip install notebook
```
```
jupyter notebook --generate-config
```
```
jupyter notebook password
```
```
nohup jupyter notebook --ip=0.0.0.0 --allow-root &
```
```
copy public Ip of your ec2 instance and paste it in browser with 8888 port    "http://54.174.165.80:8888"
'''
'''

python app.py
```
```
http://<public-ip>:5000/predict?s1=-0.96666522&s2=0.32786912&s3=-0.93579507&s4=-0.91104225&s5=0.60962671&s6=0.36569592&s7=-0.10914833&s8=-0.62181482&s9=-0.63860111&s10=0.53651178&s11=-0.46379509&s12=0.5132434&s13=-0.45632075&s14=-0.59189989&s15=0.67370318&s16=1.26928541&s17=2.17185315&s18=1.12535098&s19=0.64821758&s20=1.09244461&s21=-0.96440581&s22=-0.08750638&s23=-0.94145109&s24=-0.84547739&s25=-0.07511418&s26=-0.01862761&s27=-0.10400188&s28=-0.47718048&s29=-0.5634723&s30=0.05526303
```
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```
```
sudo apt install unzip
```
```
unzip awscliv2.zip
```
```
sudo ./aws/install
```
```
sudo apt install docker.io -y
```
```
sudo systemctl start docker 
```
```
sudo chmod 777 //var/run/docker.sock
```
```
pip install --upgrade awscli
```
```
aws configure
'''
'''
aws configure --profile <your_docker_profile_name>
```
### Log into your AWS Console and open the Amazon ECR service.
### Create a new repository cancer-repository 
#### visibility setting = public
#### repository name = cancer-repository
#### Create 

### Click the repository name and view push commands, copy the all 4 commands and paste into terminal


### the file looking like that I mention in below 
```
sudo aws ecr get-login-password --region ap-southeast-2 | docker login --username AWS --password-stdin <AWS Account Number>.dkr.ecr.ap-southeast-2.amazonaws.com
```
```
docker build -t cancer-proj . #Build docker Image with name cancer-proj
```
```
docker tag cancer-proj:latest <AWS Account Number>.dkr.ecr.ap-southeast-2.amazonaws.com/cancer-repository:lates
```
```
docker push <AWS Account Number>.dkr.ecr.ap-southeast-2.amazonaws.com/cancer-repository:latest # push the Image to Amazon ECR Repository
```
### The Docker Image with Image tag latest is now available for use in the cancer-repository
## Deploying CancerApp on Amazon ECS
### Creating Amazon ECS Cluster
##### Open the Amazon ECR service.
##### Creation of a Cluster named CancerAppCluster
##### Infrastructure = AWS Fargate (serverless)
### Create 
#### Finally, a Cluster CancerAppCancer has been created with Fargate 
### Creating a new Task definition
#### Click create a new Task definition
Task definition family - give the name
Infrastructure requirement - 
##### Launch type = AWS Fargate 
OS, Architecture, Network mode keep default
##### Task role = ExecutionRole
#### Container - 1 
##### Name = give the you just created the cluster name
##### image URL = Paste the URL 
##### Add port = 5000 (In port mappings) - TCP -HTTP
####Resource allocation limits - conditional  optional
####untick use log collection box 
####other setting -default 
### Create
## Testing the CancerApp
### when you running the task in the network setting metion the all traffic or 5000 port then after run the task
### click on create Task defination - Click on Deploy - Run Task - select existing created cluster -compute configuration - select capacity provider strategy - Capacity provider -Fargete -Deployment configuration- Application type -Task -Desired tasks -1 -In Networking - select created security group - other setting default - create

### After Task is running open it and click on configuration file and copy the public ip 
```
http://<public-ip>:5000/predict?s1=-0.96666522&s2=0.32786912&s3=-0.93579507&s4=-0.91104225&s5=0.60962671&s6=0.36569592&s7=-0.10914833&s8=-0.62181482&s9=-0.63860111&s10=0.53651178&s11=-0.46379509&s12=0.5132434&s13=-0.45632075&s14=-0.59189989&s15=0.67370318&s16=1.26928541&s17=2.17185315&s18=1.12535098&s19=0.64821758&s20=1.09244461&s21=-0.96440581&s22=-0.08750638&s23=-0.94145109&s24=-0.84547739&s25=-0.07511418&s26=-0.01862761&s27=-0.10400188&s28=-0.47718048&s29=-0.5634723&s30=0.05526303
```
## Hurray! finally my CancerApp is in operation. Now when we copy the URL in the browser, it predicted the result as ‘0’ which means a patient is diagnosed as Benign for breast cancer.
# preferred link for more information

https://srinipratapgiri.medium.com/deployment-of-containerized-machine-learning-model-application-on-aws-elastic-container-cbd1464643b3

