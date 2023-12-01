pipeline {
    agent any
    
    stages {
        stage("Compilation") {
            steps {
                script {
                    echo "Étape de compilation..."
                    sh "./gradlew compileJava"
                }
            }
        }
        
        stage("Test unitaire") {
            steps {
                script {
                    echo "Exécution des tests unitaires..."
                    sh "./gradlew test"
                }
            }
        }
    }
}

