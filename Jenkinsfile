node {
    def app
    
    stage('Clone repository') {  
        checkout scm
    }
    
    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'jenkins-github-access-token2', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                        sh '''
                        git config user.name "joaquimcampos"
                        git config user.email "joaquimcampos@duck.com"
                        cat vote-ui-deployment.yaml
                        sed -i 's+jcampos15/vote.*+jcampos15/vote:${DOCKERTAG}+g' vote-ui-deployment.yaml
                        cat vote-ui-deployment.yaml
                        git add .
                        git commit -m 'Done by Jenkins Job deployment: ${env.BUILD_NUMBER}' || echo "Nothing to commit"
                        git push https://$GIT_USERNAME:$GIT_PASSWORD@github.com/$GIT_USERNAME/vote-deploy.git HEAD:master
                        '''
                    }
                }
            }
    }
} 
