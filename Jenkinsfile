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
                        sh 'git checkout master'
                        sh 'git merge test'
                        sh 'git commit -am "Merged develop branch to master'
                        withCredentials([sshUserPrivateKey(credentialsId: 'jenkins_test', keyFileVariable: 'SSH_KEY')]) {
                           sh("git push origin master")
                           }
                    }
                }
            }
        }
    }
