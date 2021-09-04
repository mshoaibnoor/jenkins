pipeline{
    agent any
    stages{
        stage('checkout'){
            steps{
                sh 'rm -rf *'
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/osmanshaikhSystemsltd/simple-java-maven-app.git']]])
            }
        }
        stage('maven build'){
            when{
                branch 'dev'
            }
            steps{
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                // sh 'mvn test -Dtest=AppTest'
                // sh 'mvn test -Dtest=AppTest2'
            }
            post {
                always {
                    // junit 'target/surefire-reports/*.xml'
                    junit healthScaleFactor: 2.0, testResults: 'target/surefire-reports/*.xml'
                }
                failure{
                    echo "TEST FAILED"
                }
                success{
                    echo "TEST PASSED"
                }
            }
        }
    }
}