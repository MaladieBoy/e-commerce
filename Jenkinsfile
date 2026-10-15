pipeline {
    agent any

    environment {
        JAVA_HOME  = '/usr/lib/jvm/java-21-openjdk-amd64'
        MAVEN_HOME = '/usr/local/src/maven'
        PATH       = "${MAVEN_HOME}/bin:${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh 'cp target/e-commerce.war /opt/tomcat/latest/webapps/'
            }
        }

        stage('Verify') {
            steps {
                sh 'sleep 15'
                sh 'curl -fsL -o /dev/null -w "HTTP %{http_code}\\n" http://localhost:8080/e-commerce/'
            }
        }
    }

    post {
        success { echo 'Deployed: http://localhost:8080/e-commerce' }
        failure { echo 'Pipeline failed, check the stage that turned red.' }
    }
}
