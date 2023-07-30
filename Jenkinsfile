node {
    def app
    
    env.IMAGE = 'menaps4life/amazon-app'

    stage('Clone repository') {
             git branch: 'main', url: 'https://github.com/Menaps4life/argocd-manifest.git'  
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'ndoh-github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //script {def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')}
                        //script  {def IMAGE='ooghenekaro/nodejs-app'}
                        sh "git config user.email ndohnaps2@gmail.com"
                        sh "git config user.Menaps4life"
                        //sh "git switch master"
                        sh "cat deployment.yml"
                        sh "sed -i 's+${IMAGE}.*+${IMAGE}:${DOCKERTAG}+g' deployment.yml"
                        sh "cat deployment.yml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/argocd-manifest.git HEAD:main"
             }
         }
     }
  }
}
