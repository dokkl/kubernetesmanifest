node {
    def app

    stage('Clone repository') {


        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email dokkl@naver.com"
                        sh "git config user.name hoon"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+dokkl/hello-jib.*+dokkl/hello-jib:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}: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@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
//                         sh "git push https://github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}