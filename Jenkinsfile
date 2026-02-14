pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }
    stages {
        stage("build") {
            steps {
                echo "----build started-----"
                sh 'mvn clean package -Dmaven.test.skip=true'
                echo "-----build completed-------"
            }
        }
        stage("test") {
            steps {
                echo "----test started-----"
                sh 'mvn surefire-report:report'
                echo "-----test completed-------"
            }
        }
        
        stage("SonarQube analysis") {
            environment {
                scannerHome = tool 'saidemy-sonar-scanner'
            }
            steps {
                withSonarQubeEnv('saidemy-sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
     }
}
