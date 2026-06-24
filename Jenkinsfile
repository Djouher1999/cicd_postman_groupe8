pipeline {
    agent {
        docker { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }

    stages {
        stage('lancer le test') {
            steps {
                script {
                    echo "executer la premiere collection "
                    sh "newman run collection.json"

                }
            }
        }
    }

     stages {
        stage('lancer le job') {
            steps {
                script {
                    build job :'jenkinsfille2', wait : true
                }
            }
        }
    }

    
}