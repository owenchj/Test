  pipeline {
        agent any
        stages{
            stage("Compile") {
                steps {
                    script {
                        echo "Compiling..."
                    }
                }
            }
            stage("Test") {
                steps {
                    script {
                        echo "Testing..."
                    }
                }
            }
            stage("Build") {
                steps {
                withCredentials([usernamePassword(credentialsId: 'jenkins_test', usernameVariable: 'username', passwordVariable: 'password')]){
                sh("ssh-keygen -b 4096 -t rsa -f ~/.ssh/rsa_jenkins -q -N $password")
                sh("git checkout test")
                sh("git pull")
                sh("git checkout master")
                sh("git pull")
                sh("git merge test")
                sh("git push http://$username:$password@github.com/owenchj/Test.git master")
                }
                // withCredentials([sshUserPrivateKey(credentialsId: 'jenkins_test', keyFileVariable: 'SSH_KEY')]) {
                // sh("git checkout test")
                // sh("git pull")
                // sh("git checkout master")
                // sh("git pull")
                // sh("git merge test")
                // sh("git push origin master")
                // }
                }
            }
        }
    }
