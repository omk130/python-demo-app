pipeline {                                // Starts the Jenkins Declarative Pipeline

    agent any                             // Jenkins needs a machine (agent/node) to execute the pipeline

    stages {                              // pipeline is divided into stages

        stage('Checkout') {               // stage name
            steps{                        // Contains commands Jenkins will execute.
                git branch: 'main',
                url: 'https://github.com/omk130/python-demo-app.git'
            }
        }

        stage('Setup Python') {       
            steps{                            // sh means execute shell commands on linux/unix agents
                bat '''                        
                python -m venv env
                venv\Scripts\activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }


        stage('Run tests') {
            steps{
                bat '''
                venv\Scripts\activate
                pytest                          // Pytest searches for "tests" directory and then runs test.py

                '''
            }
        }



        stage('Build Package') {
            steps{
                bat '''
                venv\Scripts\activate
                pip install build                 // Uses python build tool to read configuration from setup.py
                '''
            }
        }


        stage('Archive Artifacts') {                // Save build outputs inside Jenkins
            steps{
                archiveArtifacts artifacts: 'dist/*' , fingerprint: true         // Archive every file inside the dist directory. fingerprint: true means Generates unique fingerprints (hashes) for files.
            }
        }



    }

}