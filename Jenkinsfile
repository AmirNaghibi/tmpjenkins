/** Simple pipeline to: 
    1. Compile java source files
    2. Extract class files into a directory
    3. Archive the class files and make them available as build artifact
*/

pipeline{
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
                    zip(zipFile:"../simpleprogram", archive:true, dir:"./", glob:"*.class")
                }
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