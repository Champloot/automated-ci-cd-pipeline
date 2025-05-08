pipeline {
  agent any
  stages {
    stage('Deploy') {
      steps {
        sh """
          ssh -o StrictHostKeyChecking=no \
              -i /var/lib/jenkins/.ssh/id_rsa \
              vagrant@192.168.56.11 \
              'ansible-playbook -i ansible/inventory.ini ansible/deploy.yml'
        """
      }
    }
  }
}
