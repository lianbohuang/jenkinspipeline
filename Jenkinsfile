pipeline {
    agent any

    tools { 
        maven 'localMaven' 
    }
    
    parameters { 
         //string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '52.15.230.24', description: 'Production Server')
    } 

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

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
    stage ('Deploy to prod'){
        //steps {
        //    timeout(time:5, unit:'DAYS') {
        //        input message: 'Approve PRODUCTION deployment?'
        //    }
        //    echo 'Deploying to prod...'
        //    build job: 'deploy-to-prod'
        //}
        steps {
            echo 'Deploying to prod...'
            sh "scp -i /home/robert/Downloads/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
        }
        post {
            success {
                echo 'Deploying to prod successful'
            }
            failure {
                echo 'Deploying to prod failed'
            }
        }

    }
}
}
