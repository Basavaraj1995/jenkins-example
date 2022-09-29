pipeline {
    agent any
	environment {
    AWS_ACCESS_KEY_ID = 'AKIA6AZWZ6EJZCQYXJWZ'
    AWS_SECRET_ACCESS_KEY = '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'
    AWS_REGION = 'ap-south-1'
}

    /*tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
        mvn -version
    }*/

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/Basavaraj1995/jenkins-example.git'

                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
		//sh "aws s3 ls"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
		  stage('s3 copy') {
             steps {
		     script {
          withCredentials([usernamePassword(
            passwordVariable: 'AWS_SECRET_ACCESS_KEY',
            usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
		          sh "aws s3 ls"
			 //sh "aws s3 cp file.txt s3://bucket-name"
            
            }
            }
			 
                
            }
        }		  
    }
}
