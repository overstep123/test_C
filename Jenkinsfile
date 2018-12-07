pipeline {
    agent any
    docker{
        image 'maven:3.3.3'
        args  '-it'
            steps{
                sh 'touch test.txt' 
            }
        stage('Checkout') {
            steps {
                echo 'Checkout'
                checkout([$class: 'GitSCM', branches: [[name: 
'*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], 
submoduleCfg: [], userRemoteConfigs: [[credentialsId: 
'fa085717-bebd-47db-9ceb-d850d80ca45e', url: 
'https://github.com/overstep123/test_C.git']]])
            }
        }       
        stage('Build') {
            steps {
                echo 'Building'
                sh 'cd /root/.jenkins/workspace/test3/ && gcc main.c -o main' 
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
                sh 'cd /root/.jenkins/workspace/test3/ && ./main' 
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
                sh 'cd /root/.jenkins/workspace/test3/ && scp -o port=23 main 192.168.211.1:/root'  
            }
        }
    }
}

