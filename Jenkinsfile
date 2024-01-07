
pipeline {
    agent {
        label 'maven'
    } 
environment {
    PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
}
    stages {
        
        stage("build"){
            steps {
                 echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                 echo "----------- build complted ----------"
            }
        }

        stage("Test"){
            steps{
                echo "-------------Unit test started--------------"
                sh 'mvn surefire-report:report'
                echo "-------------Unit test completed"
            }
        }

        stage('SonarQube Analysis') {

        environment {
           scannerHome = tool 'sonar-scanner'

            }
        steps {
                
            withSonarQubeEnv('sonarqube-server') {
                        // Run the SonarQube analysis
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                
            }
        }
        
        }

}

    