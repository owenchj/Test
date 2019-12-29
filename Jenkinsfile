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
                        sh 'git push origin master'
                    }
                }
            }
        }
    }
