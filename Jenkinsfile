@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Hello groovy") {
            steps {
                script {
                    Output.hello(this, "groovy")
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
