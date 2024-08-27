pipeline {
    agent {
        label 'agent'
    }
   
    options {
      gitLabConnection('gitlab')
      gitlabCommitStatus(name: 'jenkins')
    }
    triggers {
        gitlab(triggerOnPush: true, triggerOnMergeRequest: true, branchFilterType: 'All')
    }
    stages {
        stage('Get Code') {
            steps {
                checkout scm // Get some code from a GitHub repository
            }
        }
        stage('Unit tests') {
            steps {
                echo "Unit Tests"
            }
        }
        stage('Sonarqube analysis') {
            steps {
                echo "Sonarqube analysis"
            }
        }
        stage('Build application docker image') {
            steps {
                echo "Build application docker image"
            }
        }
        stage ('Pushing image to docker registry') {
            steps {
                echo "Build application docker image"
            }
        }
    }
    post {
        success {
            withCredentials([string(credentialsId: 'gitlab', variable: 'GITLAB_TOKEN')]) {
                sh """
                curl -X POST \
                     -F token=$GITLAB_TOKEN \
                     -F ref=main \
                     http://gitlab/api/v4/projects/1/trigger/pipeline
                """
            }
        }
        always {
            echo "Gather test results"
            echo "Cleanup"
            updateGitlabCommitStatus name: 'build', state: currentBuild.resultIsBetterOrEqualTo('SUCCESS') ? 'success' : 'failed'
        }
    }
}


 
