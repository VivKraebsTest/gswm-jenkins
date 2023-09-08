pipeline {
    agent { docker { image 'maven:3.9.4-eclipse-temurin-17-alpine' } }
    parameters{
        string(name: 'specialParam', 
               defaultValue: 'Test!',
               description:'String Test Param')
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        /* Pro Umgebung "Entwicklung, Test, Prod" ein Branch. */
        stage('deploy test') {
            when {
                branch 'test'
            }
            steps {
                //sh './deploy.sh OMSTA'
                echo 'Ich bin im Test! Mit dem Param ${specialParam}'
            }
        }

        stage('deploy master') {
            when {
                branch 'master'
            }
            steps {
                // Stoppen der Anwendung
                // evtl. REST-Aufruf / Skript-Aufruf
                //curl 'http://omspneu.apps-p.d001.loc:4712/shutdown'
                //sh './stop_omsrealtime.sh'
                // Deployment des neuen Releases
                /* Deployment-Skripte mit Namenskonventionen für Konfig-Ordner:
                        cfg_$HOSTNAME/config.xml
                        ...
                    oder:
                        cfg/$HOSTNAME/config.xml
                        ...
                */
                //sh './deploy.sh OMSPNEU'
                // Start der Anwendung
                //sh './start_omsrealtime.sh'
                echo 'Ich bin im Master!'
            }
        }
    }
    post {
        always {
            echo 'Ich bin fertig!'
            deleteDir()
            echo 'Verzeichnis gelöscht.'
        }

        failure {
            echo 'Ich hab ein Problem!'
            deleteDir()
            echo 'Verzeichnis gelöscht.'
        }
    }
}
