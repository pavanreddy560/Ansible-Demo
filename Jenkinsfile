pipeline {
   
   tools {
        maven 'Maven3'
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AbdulShukur007/Ansible-demo.git']]])
            }
        }  
        stage('Maven Build'){
            steps {
                sh 'mvn clean install'           
            }
        }
        stage('Ansible Script'){
             steps {
                 ansiblePlaybook disableHostKeyChecking: true, installation: 'ansible2', inventory: 'myhosts.inv', playbook: 'ansible.yml'
             }
        }  
          
    }
 }
