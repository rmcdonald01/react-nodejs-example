pipeline {
    agent any
    stages {
        stage('init') {
            steps {
                script {
                    echo 'init'
                    //gv = load "script.groovy"
                }
            }

        }
        stage("build") {
            steps {
                script {
                    echo 'build app'
                    //gv.buildJar()
                }
            }

        }
        stage("build image") {
            steps {
                script {

                    echo 'building the docker image...'
                    withCredentials([
                        usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')
                                    ]) {
                        sh 'docker build -t ramon101/my-java-repo:webapp-1.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push ramon101/my-java-repo:webapp-1.0'
                                    }
                }
            }

        }
        stage("deploy") {
            steps {
                script {
                    echo 'deploying ec2'
                    def dockerCmd = 'docker run -p -d 3080:3080 ramon101/my-java-repo:webapp-1.0'
                    sshagent(['ec2-server-key']) {
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@3.143.208.228 ${dockerCmd}"
                }
                }
            }
        }
    }
}