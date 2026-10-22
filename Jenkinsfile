pipeline {
    agent any

    stages {
        stage('Install dependencies') {
            when {
                anyOf {
                    branch 'GH-Devop'
                    branch 'Jenkins-Devop'
                }
            }
            
            steps {
                
                echo 'Installing node modules ...'
                bat 'npm install'
                
                echo 'Installing Playwright ...'
                bat 'npx playwright install'
            }
        }

        stage('Run servers and tests') {
            when {
                anyOf {
                    branch 'GH-Devop'
                    branch 'Jenkins-Devop'
                }
            }
            
            steps {
                bat '''
                    echo Starting backend ...
                    start /B cmd /C "npm run server"

                    echo Starting frontend ...
                    start /B cmd /C "npm run start"

                    echo Waiting for servers to start ...
                    timeout /t 10 /nobreak

                    echo Running tests ...
                    npm test
                '''
            }
        }
    }
}