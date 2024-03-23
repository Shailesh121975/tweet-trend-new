pipeline {
    agent {
        node {
            label 'maven'
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }
    stages {
        stage("build") {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean deploy'
                echo "----------- build completed ----------"
            }
        }
        stage('SonarQube analysis') {
            environment {
                env.JAVA_HOME = "${tool 'java-11-openjdk'}"
                env.PATH = "${env.JAVA_HOME}/bin:" + "${env.PATH}"
                scannerHome = tool 'DevopsShankarSonarQube-Scanner'
            }
            steps {
                withSonarQubeEnv('DevopsShankarSonarQube-Server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
