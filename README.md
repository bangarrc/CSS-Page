git clone repo
sudo apt install docker.io / sudo snap install docker
sudo chown $USER path
create Dockerfile in project folder
Dockerfile===>
 # Stage 1

FROM node:18 as builder

WORKDIR /build

COPY package*.json .
RUN npm install

COPY src/ src/
COPY tsconfig.json tsconfig.json

RUN npm run build

# Stage 2

FROM node:18 as runner

WORKDIR /app

COPY --from=builder build/package*.json .
COPY --from=builder build/node_modules node_modules/
COPY --from=builder build/dist dist/

CMD [ "npm", "start" ]

docker build -t 1-tier .
docker run -d -p 8000:8000 1-tier-backend

@AWS CLI configuration
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip
unzip awscliv2.zip
sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin --update
aws configure

@IAM Configuration

Create a user eks-admin with AdministratorAccess.
Generate Security Credentials: Access Key and Secret Access Key.
Access key-AKIAQ3EGVZCNCHI2OWFJ
Secrete access key-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

@PUSH docker image to ECR
Repo name= 1-tier-backend
commands are available in repo= push commands button

@ECS Cluster
Create ECS cluster
Create Task definition & add docker image to task
Create Service in cluster & add task to service

If you updated any code change & then to implement that change to your prod follow steps
===>First build docker image==>Tag image & push to ECR 
===>GO to service==>update service==>click checkbox=force deployment==>

@To delete cluster==>update service==>change desired task to 0==>delete service==>select cluster==>delete task definition 
