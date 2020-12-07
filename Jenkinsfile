pipeline {
    agent {
        label 'Tomcat'
    }
    tools {
        maven 'Maven'
    }
    stages {
        stage ('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/Aravindkrishnans/branch_test.git']]])
            }
        }
        stage ('build') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'Tomcat', path: '', url: 'http://13.234.77.241:8080/')], contextPath: 'build_trigger_job', war: '**/*.war'
            }
        }
    }
post {
    success {
        echo "The Build is success"
    }
}
}
