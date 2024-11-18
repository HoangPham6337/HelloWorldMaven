pipeline {
    agent any
    stages{
        stage('Application retrieval') {
            steps {
                git branch: 'master',
                credentialsId: 'hoang6337',
                url: 'https://github.com/HoangPham6337/HelloWorldMaven'
            }
        }
        
        stage('Application clean') {
            steps {
                withMaven(maven : 'apache-maven-3.6.0') {
                    sh "mvn clean"
                }
            }
        }
        
        stage('Application build') {
            steps {
                withMaven(maven : 'apache-maven-3.6.0') {
                    sh "mvn package"
                }
            }
        }
        
        stage("Tag Version. Release") {
            environment {
                GIT_TAG = "Version-2.$BUILD_NUMBER"
            }
            steps {
                script {
                    // Set Git configurations
                    sh 'git config user.name "HoangPham6337"'
                    sh 'git config user.email "hoangpham4171@gmail.com"'
                    
                    // Tagging the repository
                    sh "git tag -a ${GIT_TAG}"
                    
                    // Push the tag to the repository securely
                    withCredentials([usernamePassword(credentialsId: 'hoang6337', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                        sh "git push https://github.com/HoangPham6337/HelloWorldMaven ${GIT_TAG}"
                    }
                }
            }
        }
    }
}
