def registry = 'https://vigilantfiesta.jfrog.io'

pipeline{
    agent{
        node{
            label 'maven-slave'
        }
    }

    environment {
        PATH = "/opt/apache-maven-3.9.5/bin:$PATH"
    }

    stages{
        stage("Build"){
            steps {
                echo "---------Build Started-------------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "---------Build Completed------------"
            }
        }
        stage("Unit Test"){
            steps{
                echo "------------Unit test started--------------"
                sh 'mvn surefire-report:report'
                echo "------------Unit test completed------------"
            }
        }
        // stage ("Sonarqube Analysis"){
        //     environment{
        //         scannerHome = tool 'sonar-scanner'
        //     }
        //     steps{
        //         withSonarQubeEnv('sonar-server'){
        //             sh '${scannerHome}/bin/sonar-scanner'
        //         }
        //     }
        // }
        // stage ("Quality Gate"){
        //     steps{
        //         script{
        //             timeout(time: 1, unit: 'HOURS'){
        //                 def qg = waitForQualityGate()
        //                 if (qg.status != 'OK'){
        //                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
        //                 }
        //             }
        //         }
        //     }
        // }
        stage ("Publish Jar to JFrog Artifactory"){
            steps{
                script{
                    echo "---------------Jar Publish started----------------------"
                    def server = Artifactory.newServer url:registry+"/artifactory", credentialsId:"artifact-cred"
                    def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                    def uploadSpec = """{
                        "files": [
                            {
                              "pattern": "jarstaging/(*)",
                              "target": "libs-release-local/{1}",
                              "flat": "false",
                              "props" : "${properties}",
                              "exclusions": [ "*.sha1", "*.md5"]
                            }
                        ]
                    }"""
                    def buildInfo = server.upload(uploadSpec)
                    buildInfo.env.collect()
                    server.publishBuildInfo(buildInfo)
                    echo "----------------Jar Publish Completed-----------------------"
                }
            }
        }
    }
}