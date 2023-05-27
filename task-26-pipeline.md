- Created the simple pipeline for echoing the mesaage

~~~~~~~~~~~~~~~~~~~~~
pipeline {
    
    agent any
    stages {
        stage("print message") {
            steps {
                echo "hello world"
            }
            
        }
        
        stage('finish script') {
            steps {
                echo "this is end of build"
            }
        }
    
    }
}

~~~~~~~~~~~~~~~~~~~~~
