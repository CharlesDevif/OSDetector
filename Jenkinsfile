pipeline {
    agent any
    stages {
        stage('Clonage du dépôt GitHub') {
            steps {
                // Clonage de la branche "main" depuis votre dépôt
                git branch: 'main', url: 'https://github.com/CharlesDevif/OSDetector.git'
            }
        }
        stage('Installer Python et pip') {
            steps {
                // Mettre à jour la liste des paquets et installer python3.11 et pip
                sh '''
                   sudo apt-get update &&
                   sudo apt-get install -y python3 python3-pip
                '''
            }
        }
        stage('Exécuter le script Python') {
            steps {
                // Exécution du script, ici supposé s'appeler "script.py"
                sh 'python3 os_detector.py'
            }
        }
    }
    post {
        success {
            // En cas de succès, envoyer un mail de notification
            mail to: 'charlesdevif@hotmail.fr',
                 subject: "Build Jenkins réussie pour ${env.JOB_NAME}",
                 body: "La build a réussi ! Consultez le console output pour plus de détails."
        }
        failure {
            // En cas d'échec, envoyer un mail d'alerte
            mail to: 'charlesdevif@hotmail.fr',
                 subject: "Build Jenkins échouée pour ${env.JOB_NAME}",
                 body: "La build a échoué. Veuillez consulter le log pour identifier le problème."
        }
    }
}
