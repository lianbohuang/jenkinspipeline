pipeline {
    agent any

    tools { 
        maven 'localMaven' 
    }
    
    //parameters { 
    //     string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
    //     string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
    //} 

    //triggers {
    //     pollSCM('* * * * *') // Polling Source Control
    // }

stages{
	stage(‘Init’){
	    steps {
		    echo 'Testing…'
            sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
	    }
	}

    stage('Build'){
        steps {
		    echo 'Building…'
            sh 'mvn clean package'
        }
        post {
            success {
                echo 'Now Archiving...'
                archiveArtifacts artifacts: '**/target/*.war'
            }
        }
    }

        stage ('Deploy to Staging'){
            steps {
            	echo 'Deploying...'
                build job: 'deploy-to-staging'
            }

        }
    }
}
