pipeline {
    agent any
    
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
		echo ‘Testing…’
	    }
	}

        stage('Build'){
            steps {
                //sh 'mvn clean package'
		echo ‘Building…’
            }
            //post {
                //success {
                //    echo 'Now Archiving...'
                //    archiveArtifacts artifacts: '**/target/*.war'
                //}
            //}
        }

        stage ('Deploy'){
            steps {
            	echo ‘Code deployed.’
            }

        }
    }
}