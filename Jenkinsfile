pipeline {
agent {
label 'Build-Ansible-Server'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/devops8th/account-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/devops8th/account-service; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/devops8th/account-service ; sudo  docker login -udeploymenthub -pSateeshAnu_1904 "
        sh "cd /home/ubuntu/workspace/devops8th/account-service ; sudo docker tag account-service deploymenthub/account-service "
        sh "cd /home/ubuntu/workspace/devops8th/account-service ; sudo docker push deploymenthub/account-service  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node (' Ansible-server') {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}
    
    
}
