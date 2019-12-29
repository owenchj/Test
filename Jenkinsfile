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
                withCredentials([sshUserPrivateKey(credentialsId: 'jenkins_test', keyFileVariable: 'SSH_KEY')]) {
                sh("rm -rf ../Test")
                sh("git clone git@github.com:owenchj/Test.git")
                sh("cd Test")
                sh("git checkout test")
                sh("git pull")
                sh("git checkout master")
                sh("git pull")
                sh("git merge test")
                sh("git push origin master")
                }
                }
            }
        }
    }
