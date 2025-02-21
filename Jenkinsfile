pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''#!/bin/bash
                echo 'In C or Java, we can compile our program in this step'
                echo 'In Python, we can build our package here or skip this step'
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''#!/bin/bash
                echo 'Test Step: Running pytest'
                
                # Use the conda installation in Jenkins home directory
                CONDA_PATH="/var/lib/jenkins/miniconda3/bin/conda"
                
                if [ ! -f "$CONDA_PATH" ]; then
                    echo "Error: Conda not found at $CONDA_PATH"
                    exit 1
                fi
                
                echo "Found conda at: $CONDA_PATH"
                
                # Initialize conda in the current shell
                eval "$($CONDA_PATH shell.bash hook)"
                
                # Run pytest in the mlip environment
                $CONDA_PATH run -n mlip pytest
                '''
            }
        }
        stage('Deploy') {
            steps {
                echo 'In this step, we deploy our project'
                echo 'Depending on the context, we may publish the project artifact or upload pickle files'
            }
        }
    }
}