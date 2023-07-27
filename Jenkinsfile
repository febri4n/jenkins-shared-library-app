@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Maven build") {
            steps {
                script {
                    maven("clean compile")
                }
            }
        }
        stage("Global variable") {
            steps {
                script {
                    echo(author())
                    echo(author.name())
                    echo(author.jobs())
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
