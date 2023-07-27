@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Output;

pipeline {
    agent any
    stages {
        stage("Hello person") {
            steps {
                script {
                    hello.person([
                        firstName: "Febrian",
                        lastName: "Saputra"
                    ])
                }
            }
        }
        stage("Maven build") {
            steps {
                script {
                    maven(["clean","compile","test"])
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
