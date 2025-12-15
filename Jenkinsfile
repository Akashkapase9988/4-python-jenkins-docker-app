pipeline {
    agent any
    stages {
        stage('Clone Github Repository') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/Akashkapase9988/4-python-jenkins-docker-app.git'
                sh 'pwd'
            }
        }        
        stage('Build') {
            steps {
                    sh 'python3 -m py_compile app.py'
                
            }
        }
        stage('Test') {
            steps {
                    sh 'python3 -m unittest discover tests'
                
            }
        }
        stage('Docker Build') {
            steps {
                    sh 'docker build -t python-app:latest .'
                
            }
        }
        stage('Docker Run') {
            steps {
                    sh 'docker run --rm python-app:latest'
                
            }
        } 
        stage('Docker Tag & Push') {
            steps {
                
                    withCredentials([usernamePassword(credentialsId: 'akashk9988', passwordVariable: 'Dockerhubpassword', usernameVariable: 'Dcokerhubuser')]) 
 {
                        sh '''
                            echo "$Dockerhubpassword" | docker login -u "$Dcokerhubuser" --password-stdin
                            docker tag python-app:latest akashk9988/python-app:v12
                            docker push akashk9988/python-app:v12
                        '''
                    }
                
            }
        }         
    }
    post {
        always {
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
sysnytax
