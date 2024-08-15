pipeline {
    agent {
        label 'ansible-controller'
    }
    stages {
        stage('Print Environment Variables') {
            steps {
                script {
<<<<<<< HEAD
                    // Imprimir todas las variables de entornoo
=======
                    // Imprimir todas las variables de entorno
>>>>>>> 997e1625336868aed2a08480e46148d44d2f6aa7
                    env.each { key, value ->
                        echo "${key} = ${value}"
                    }
                }
            }
        }
        stage('Preparation') {
            steps {
                script {
                    // Definir el entorno en función de la branch
                    if (env.BRANCH_NAME == 'dev') {
                        env.INVENTORY = 'ansible/inventories/dev/host.ini'
                    } else if (env.BRANCH_NAME == 'staging') {
                        env.INVENTORY = 'ansible/inventories/staging/host.ini'
                    } else if (env.BRANCH_NAME == 'main') {
                        env.INVENTORY = 'ansible/inventories/main/host.ini'
                    }
                }
                echo "Using inventory: ${env.INVENTORY}"
            }
        }
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Copy Files') {
            steps {
                script {
                    // Crear directorios en el agente remoto
                    sh 'mkdir -p ~/ansible/inventories/dev'
                    sh 'mkdir -p ~/ansible/inventories/staging'
                    sh 'mkdir -p ~/ansible/inventories/main'
                    sh 'mkdir -p ~/ansible/playbook'
                    // Copiar los archivos necesarios al agente remoto
                    sh 'cp ${WORKSPACE}/ansible/inventories/dev/host.ini ~/ansible/inventories/dev/'
                    sh 'cp ${WORKSPACE}/ansible/inventories/staging/host.ini ~/ansible/inventories/staging/'
                    sh 'cp ${WORKSPACE}/ansible/inventories/main/host.ini ~/ansible/inventories/main/'
                    sh 'cp ${WORKSPACE}/ansible/playbook/playbook.yml ~/ansible/playbook/'
                }
            }
        }
        stage('Run Playbook') {
            steps {
                sh """
                ansible-playbook -i ~/${env.INVENTORY} ~/ansible/playbook/playbook.yml --ssh-extra-args='-o StrictHostKeyChecking=no'
                """
            }
        }
    }
}
