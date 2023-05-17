pipeline {
    agent any
    tools{
        maven 'maven3.9.2'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/gravindra85/firstdevopsproject']]])
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    bat 'docker build -t gravindra85/first_devops_project .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                   bat 'docker login -u gravindra85 -p ${dockerhubpwd}'
                   }
                   bat 'docker push gravindra85/first_devops_project'
                }
            }
        }
        //stage('Deploy to k8s'){
           // steps{
                //script{
                    //kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
               //}
            //}
        //}
    }
}