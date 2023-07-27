@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Ouput;

pipeline {
    agent any
    stages {
        stage("Hello groovy") {
            steps {
                script {
                    Ouput.hello("groovy")
                }
            }
        }
        stage("Hello world") {
            steps {
                script {
                    hello.world()
                }
            }
        }
    }
}
