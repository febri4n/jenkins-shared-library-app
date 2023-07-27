@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Global variable") {
            steps {
                script {
                    echo(author.name())
                    echo(author.channel())
                }
            }
        }
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
