pipeline {
    agent { label 'slave1' }



    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository


                // Run Maven on a Unix agent.
                sh "npm start"
              

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }


            }
    }
}
