pipeline {
    agent any
    
    environment {
        PATH = "/usr/share/maven/bin:$PATH"
    }

    triggers {
        pollSCM('* * * * *') // Schedule the pipeline to check for changes every minute
    }

    stages {
        stage('git') {
            steps {
                git 'https://github.com/pratiksnarkhede/hello-world.git'
            }
        }

        stage('build') {
            steps {
                sh "mvn clean install"
            }
        }

        stage('deploy') {
            steps {
                sshagent(['deploy_user']) {
                    sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/pipeline/webapp/target/webapp.war azureuser@20.192.0.194:/opt/tomcat/webapps"
                }
            }
        }
    }
}
