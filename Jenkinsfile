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
        stage('Artificats Upload'){
           steps {  
                    pom = readMavenPom file: "pom.xml";
                    filesByGlob = findFiles(glob: "target/*.${pom.packaging}");
                    echo "${filesByGlob[0].name} ${filesByGlob[0].path} ${filesByGlob[0].directory} ${filesByGlob[0].length} ${filesByGlob[0].lastModified}"
                    artifactPath = filesByGlob[0].path;
                    artifactExists = fileExists artifactPath;
                    if(artifactExists) {
                        echo "*** File: ${artifactPath}, group: ${pom.groupId}, packaging: ${pom.packaging}, version ${pom.version}";
           
                        nexusArtifactUploader artifacts: [[artifactId: 'LoginWebApp', classifier: '', file: 'artifactPath', type: 'war'], [artifactId: 'LoginWebApp', classifier: '', file: 'pom.xml', type: 'pom']], credentialsId: 'nexus', groupId: 'com.devops4solutions', nexusUrl: '44.203.200.106:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://44.203.200.106:8081/repository/maven-releases/', version: '1'
                    }
                        else {
                        error "*** File: ${artifactPath}, could not be found";
                    }
               }  
           }  
        } 
    }
 }
