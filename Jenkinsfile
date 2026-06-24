pipeline {
    agent {
        docker { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }

    parameters {
        booleanParam(name: 'benvironnement', defaultValue: true, description: 'avec ou sans environnement')
        choice(name: 'environnement', choices: ['aucun', 'environment2', 'environment3'], description: 'Choisissez l environnement')
        choice(name: 'collection', choices: ['collection', 'collection2', 'collection3'], description: 'Choisissez la collection')
    }

    stages {
        stage('lancer le test') {
            steps {
                script {
                    def collectionFile = "${params.collection}.json"
                    def result

                    if (params.benvironnement == 'aucun') {
                        result = sh(script: "newman run collection.json", returnStatus: true)
                    } else {
                        switch(params.environnement) {
                            case "environment2":
                                result = sh(script: "newman run ${collectionFile} --environment environment2.json", returnStatus: true)
                                break
                            case "environment3":
                                result = sh(script: "newman run ${collectionFile} --environment environment3.json", returnStatus: true)
                                break
                            default:
                                error("Environnement inconnu : ${params.environnement}")
                        }
                    }

                    if (result != 0) {
                        unstable("Newman a détecté des échecs de tests")
                    }
                }
            }
        }
    }
}