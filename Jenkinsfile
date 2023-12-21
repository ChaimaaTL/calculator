pipeline {
    agent any
    stages {
        stage("Compilation") {
            steps {
                sh "./gradlew compileJava"
            }
        }
        
        stage("Test unitaire") {
            steps {
                sh "./gradlew test"
            }
        }
        
        stage("Couverture du code") {
            steps {
            dir('home/clonecalculatore/calculator') {
                sh "./gradlew jacocoTestReport"
                
                publishHTML(target: [
                    reportDir: 'build/reports/jacoco/test/html',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Report'
                ])
                
                sh "./gradlew jacocoTestCoverageVerification"
            }
            }
        }
        
        stage("Analyse statique du code") {
            steps {
                sh "./gradlew checkstyleMain -Pcheckstyle.config=file:/home/clonecalculatore/calculator/config/checkstyle/checkstyle.xml"
                
                publishHTML(target: [
                    reportDir: 'build/reports/checkstyle/',
                    reportFiles: 'main.html',
                    reportName: 'Checkstyle Report'
                ])
            }
        }
    }
    post {
        always {
            mail to: 'chaimaa.tawil7@gmail.com',
                 subject: "Chere chaimaa, votre compilation est terminée: ${currentBuild.fullDisplayName}",
                 body: "Votre build est accompli. Veuillez vérifier: ${env.BUILD_URL}"
        }
    }
}


