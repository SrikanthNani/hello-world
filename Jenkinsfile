pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/SrikanthNani/hello-world.git'

                // Run Maven on a Unix agent.
                sh "mvn clean install"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }    
        stage('Deploy to Container') {
			   steps {
			    deploy([
				    adapters: [tomcat8(credentialsId: 'tomcat_deployer', path: '', url: 'http://34.125.29.221:8080/')],
					  contextPath: null,
					  war: '**/*.war'
				    ])
			    }
		    }
    }
}
