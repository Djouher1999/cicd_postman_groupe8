pipeline {
    agent {
        docker { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }

    parameters {
        booleanParam(name: 'benvironnement', defaultValue: true, description: 'avec ou sans environnement')
        choice(name: 'environnement', choices: ['environment2', 'environment3'], description: 'Choisissez l environnement')
        choice(name: 'collection', choices: ['collection', 'collection2', 'collection3'], description: 'Choisissez la collection')
    }

    stages {
        stage('lancer le test') {
            steps {
                script {
                    def collectionFile = "${params.collection}.json"

                    if (params.benvironnement == false) {
                        sh "newman run ${collectionFile}"
                    } else {
                        switch(collectionFile) {
                            case collection2:
                                sh "newman run ${collectionFile} --environment environment2.json"
                            break
                            case collection3:
                                sh "newman run ${collectionFile} --environment environment3.json"
                            break
                        }
                        
                    }
                }
            }
        }
    }
}