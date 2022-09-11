pipeline {
   
   tools {
        maven 'Maven3'
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                    git 'https://github.com/AbdulShukur007/Ansible-demo.git'
            }
        }  
        stage('Maven Build'){
            steps {
                sh 'mvn clean install'           
            }
        }
        stage('Ansible Script'){
             steps {
                 ansiblePlaybook credentialsId: 'f74a9c5e-9ba0-430e-860b-00ecedc4e322', disableHostKeyChecking: true, installation: 'ansible2', inventory: 'myhosts.inv', playbook: 'ansible.yml'
             }
        }  
          
    }
 }
