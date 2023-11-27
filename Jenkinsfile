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
        stage ("Sonarqube Analysis"){
            environment{
                scannerHome = tool 'sonar-scanner'
            }
            steps{
                withSonarQubeEnv('sonarqube-server'){
                    sh '${scannerHome}/bin/sonar-scanner'
                }
            }
        }
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
    }
}