#!groovy​

/** Simple pipeline to: 
    1. Compile java source files
    2. Extract class files into a directory
    3. Archive the class files and make them available as build artifact
*/

// options, environment, parameters, agent
pipeline{
    options {
        // skipDefaultCheckout()
        timestamps()
        timeout(time: 30, unit: MINUTES)
    }

    agent any
    
    stages{
        stage("Compile Source"){
            steps{
                echo "Compiling source files"
                dir("./src"){
                    sh "javac *"
                }
            }
        }

        stage("Extract Class Files"){
            steps{
                echo "Creating classes/ directory"
                dir("classes"){
                    echo "Moving .class files into "
                    sh "mv ../src/*class ."
                }
            }
        }

        stage("Archive Class files"){
            steps{
                dir("classes"){
                    echo "Zipping Class Files"
                    zip(zipFile:"../test.zip", archive:false, dir:"./", glob:"*.class") 
                }
                archiveArtifacts artifacts:"*.zip" 
            }
        }
    }

    post{
        always{
            echo "========End of Pipeline========"
        }
        success{
            echo "========pipeline executed successfully========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}