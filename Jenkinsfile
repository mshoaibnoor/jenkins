// making change to test webhook auto trigger
pipeline{
    agent {
        label maven
    }
    stages{
        stage('Build'){
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
