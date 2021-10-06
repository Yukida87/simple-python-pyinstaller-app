pipeline {
//None parameter in the agent section means that no global agent will be allocated for the entire Pipeline’s
//execution and that each stage directive must specify its own agent section.
    //agent none //none = every stage has own build agent
    stages {
        stage('Build') {
            agent {
                docker {
                    //You have to install 2 plugins: Docker plugin and Docker Pipeline
                    //This image parameter (of the agent section’s docker parameter) downloads the python:2-alpine
                    //Docker image and runs this image as a separate container. The Python container becomes
                    //the agent that Jenkins uses to run the Build stage of your Pipeline project.
                    //jenkins uses this image as node agent
                    image 'python:3.9-alpine'
                }
            }
            steps {
                //This sh step runs the Python command to compile your application and
                //its calc library into byte code files, which are placed into the sources workspace directory
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                //This stash step saves the Python source code and compiled byte code files from the sources
                //workspace directory for use in later stages.
                //stash because required in later stages - stashing
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
    }
}
