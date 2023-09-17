node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }

    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github-ofc', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email skonde@loginsoft.com"
                        sh "git config user.name saikrishnareddy09"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+106832631040.dkr.ecr.us-east-2.amazonaws.com/hash-wordpress-profile.*+106832631040.dkr.ecr.us-east-2.amazonaws.com/hash-wordpress-profile:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/hash-manifests.git HEAD:main"
                    }
                }
            }
    }
}