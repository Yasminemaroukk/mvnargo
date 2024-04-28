node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'githubtoken', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email marzouk.yasmine@esprit.tn"
                        sh "git config user.name Yasminemaroukk"
                        //sh "git switch master"
                        sh "cat deploy.yaml"
                        sh "sed -i 's+yasminemarzouk/devopsproject.*+yasminemarzouk/devopsproject:${DOCKERTAG}+g' deploy.yaml"
                        sh "cat deploy.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/mvnargo.git HEAD:main"
      }
    }
  }
}
}
