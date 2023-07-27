@Library("jenkins-shared-library@main") _

import febri4n.jenkins.Output;

mavenPipeline()

// pipeline {
//     agent any
//     stages {
//         stage("Library resources") {
//             steps {
//                 script {
//                     def config = libraryResource("config/build.json")
//                     echo(config)
//                 }
//             }
//         }
//         stage("Hello person") {
//             steps {
//                 script {
//                     hello.person([
//                         firstName: "Febrian",
//                         lastName: "Saputra"
//                     ])
//                 }
//             }
//         }
//         stage("Maven build") {
//             steps {
//                 script {
//                     maven(["clean","compile","test"])
//                 }
//             }
//         }
//         stage("Global variable") {
//             steps {
//                 script {
//                     echo(author())
//                     echo(author.name())
//                     echo(author.jobs())
//                 }
//             }
//         }
//         stage("Hello groovy") {
//             steps {
//                 script {
//                     Output.hello(this, "groovy")
//                 }
//             }
//         }
//         stage("Hello world") {
//             steps {
//                 script {
//                     hello.world()
//                 }
//             }
//         }
//     }
// }
