@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Hello groovy") {
            steps {
                script {
                    Output.hello("groovy")
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
