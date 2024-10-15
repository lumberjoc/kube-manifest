node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email jacques.beauvoir.engineering@gmail.com"
                        sh "git config user.name lumberjoc"
                        //sh "git switch master"
                        sh "cat 0-deployment.yaml"
                        sh "sed -i 's+image: lumberjoc/blog-app:[0-9]\\{1,\\}+image: lumberjoc/blog-app:${DOCKERTAG}+g' 0-deployment.yaml"
                        // sh "sed -i 's+lumberjoc/blog-app.*+lumberjoc/blog-app:${DOCKERTAG}+g' 0-deployment.yaml"
                        sh "cat 0-deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kube-manifest.git HEAD:main"
      }
    }
  }
}
}
