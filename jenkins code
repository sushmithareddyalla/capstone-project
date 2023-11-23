node{
    stage('code checkout'){
        git 'https://github.com/sushmithareddyalla/capstone-project.git'
    }
    stage('code build'){
        sh 'mvn clean package'
    }
    stage('contenarizing app'){
        sh 'docker build -t sushmitha1995/insure-me:1.0 .'
    }
    stage('push to docker hub'){
        withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
            sh "docker login -u sushmitha1995 -p ${dockerhubpwd}"
            sh 'docker push sushmitha1995/insure-me:1.0'
}
    }
    stage('deploy'){
        ansiblePlaybook become: true, credentialsId: 'ansible-ssh-jenkinskey', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'test-server-config.yml', vaultTmpPath: ''
        
    }
}
