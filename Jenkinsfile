pipeline {
  agent{
    docker { image 'ansible/ansible:latest' }
  }
  
  stages {
    stage('Apply Master') {
      steps {
        echo 'Apply Master ...'
        sh "ansible-playbook kube_master.yml -i '${env.MASTER}' -e 'additional_sans=${env.ADDITIONAL_SANS} advertise_address=${env.ADVERTISE_ADDRESS}'"
      }
    }
    stage('Apply Nodes') {
      steps {
        echo 'Apply Nodes ...'
      }
    }
  }
}