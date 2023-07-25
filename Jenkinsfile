pipeline {
    agent none

    environment {
        AUTHOR = "Febrian"
        BLOG = "https://febri4n.github.io/blog/"
    }

    // triggers {
    //     cron("*/5 * * * *")
    // }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    stages {
        // stage("OS Setup") {
        //     matrix {
        //         axes {
        //             axis {
        //                 name "OS"
        //                 values "linux", "windows", "mac"
        //             }
        //             axis {
        //                 name "ARC"
        //                 values "32", "64"
        //             }
        //         }
        //         excludes {
        //             exclude {
        //                 axis {
        //                     name "OS"
        //                     values "mac"
        //                 }
        //                 axis {
        //                     name "ARC"
        //                     values "32"
        //                 }
        //             }
        //         }
        //         stages {
        //             stage("OS Setup") {
        //                 agent {
        //                     node {
        //                         label "linux && java11"
        //                     }
        //                 }
        //                 steps {
        //                     echo("Setup ${OS} ${ARC}")
        //                 }
        //             }
        //         }
        //     }
        // }

        stage("Preparation") {
            parallel {
                stage("Prepare Java") {
                    agent {
                        node {
                            label "linux && java11"
                        }
                    }
                    steps {
                        echo("Prepare Java")
                        sleep(5)
                    }
                }
                stage("Prepare Maven") {
                    agent {
                        node {
                            label "linux && java11"
                        }
                    }
                    steps {
                        echo("Prepare Maven")
                        sleep(5)
                    }
                }
            } 
        }

        stage("Parameter") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "You description is ${params.DESCRIPTION}"
                echo "Your social medis is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
            }
        }
        
        stage("Prepare") {
            environment {
                APP = credentials("febrian_rahasia")
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("App User: ${APP_USR}")
                echo("App Password: ${APP_PSW}")
                sh('echo "App Password: {APP_PSW}" > "rahasia.txt"')
                echo("Author: ${AUTHOR}")
                echo("Blog URL: ${BLOG}")
                echo("Start job: ${env.JOB_NAME}")
                echo("Start build: ${env.BUILD_NUMBER}")
                echo("Branch name: ${env.BRANCH_NAME}")
            }
        }
        
        stage("Build") {
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                script {
                    for (int i = 0; i<10; i++) {
                        echo("Script ${i}")
                    }
                }

                echo("Start build")
                sh("./mvnw clean compile test-compile")
                echo("Finish build ")
            }
        }
        
        stage("Test") {
            agent {
                node {
                    label "linux && java11"
                }
            }  
            steps { 
                script {
                    def data = [
                        "firstName" : "Febrian",
                        "lastName" : "Saputra"
                    ]
                    writeJSON(file: "data.json", json: data)
                }
                echo("Start test")
                sh("./mvnw test")
                echo("Finish test ")
            }
        }
        
        stage("Deploy") {
            input {
                message "Can we deploy ?"
                ok "Yes, of course"
                submitter "vagrant,root,febrian,febri4n"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV','QA','PROD'], description: "Which Environment ?")
                }
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Deploy to ${TARGET_ENV}")
                echo("hello deploy 1")
                sleep(5)
                echo("hello deploy 2")
                echo("hello deploy 3")
            }
        }

        stage("Release") {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            agent {
                node {
                    label "linux && java11"
                }
            }
            steps {
                echo("Release it")
                withCredentials([usernamePassword(
                    credentialsId: "febrian_rahasia",
                    usernameVariable: "USER",
                    passwordVariable: "PASSWORD"
                )]) {
                    sh('echo "Release it with -u $USER -p $PASSWORD" > "release.txt"')
                }
            }
        }
    }

    post {
        always {
            echo "i always say hello again!"
        }    
        success {
            echo "ye, success"
        }
        failure {
            echo "oh no, failure"
        }
        cleanup {
            echo "dont care success or error"
        }
    }
}
