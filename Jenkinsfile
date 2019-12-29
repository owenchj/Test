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
                    script {
                        echo "Building..."
                        sh 'git checkout test'
                        sh 'git checkout master'
                        sh 'git merge test'
                        sh 'git commit -am "Merged develop branch to master"'}
                }

                withCredentials([usernamePassword(credentialsId: 'jenkins_test', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh 'echo $PASSWORD'
                echo USERNAME
                echo "username is $USERNAME"
                }
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins_test', keyFileVariable: 'SSH_KEY')]) {
                sh("echo $SSH_KEY")
                sh("git push origin master")
                }

            }
        }
    }
