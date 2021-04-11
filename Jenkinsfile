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
                    echo 'build image'
                    //gv.buildImage()
                }
            }

        }
        stage("deploy") {
            steps {
                script {
                    echo 'deploying ec2'
                    //gv.deploy()
                }
            }
        }
    }
}