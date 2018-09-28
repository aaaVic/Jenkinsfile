pipeline {
    agent none
    stages {
	stage('Pull') {
            checkout([
                $class: 'GitSCM',
                branches: [[name: '*/master']],
                extensions: [[$class: 'CloneOption', timeout: 120]],
                gitTool: 'Default',
                userRemoteConfigs: [[url: 'git@github.com:odoo/odoo.git',credentialsId:'c264a21c-4390-4e2d-830b-3bd1cc5b42b5']]
            ])
    	}
        stage('Build') {
            agent {
                docker {
                    image 'python:3.6.6'
                }
            }
            steps {
                sh 'pip install -r requirement.txt'
                sh 'python odoo-bin'
            }
        }
    }
}