pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/gnanaprakash7/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t gnanaprakash7/phpimage:v3 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push gnanaprakash7/phpimage:v3'
                }
            }
        }
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 gnanaprakash7/phpimage:v3'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 akshu20791/phpimage:v3"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.6.151 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.6.151 ${dockerCmd}"
                        
                    }
                }
            }
        }
    }
}
