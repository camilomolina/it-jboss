#!groovy

node {
    try {
        def app

        stage('Environment') {
            echo 'Environment'
            app = 'it-jboss'

            checkout scm
        }

        stage('Provisioning') {
            echo 'Provisioning'

            //ansiblePlaybook(credentialsId: 'private_key', inventory: 'inventories/a/hosts', playbook: 'my_playbook.yml')
    		    ansiblePlaybook(playbook: 'main.yml')
        }
        stage('Results') {
            echo 'Results'
        }

        currentBuild.result = 'SUCCESS'
    } catch (any) {

        currentBuild.result = 'FAILURE'
        throw any //rethrow exception to prevent the build from proceeding
    } finally {
        step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'camilo.molina.orth@gmail.com', sendToIndividuals: true])
    }

}
