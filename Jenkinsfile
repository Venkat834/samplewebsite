// pipeline {
//     agent any

//      stages {
//         stage('Clone Repository') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/Venkat834/samplewebsite.git'

//             }
//         }

//         stage('Validate HTML') {
//             steps {
//                 script {
//                     // Simple validation that the file exists
//                     if (!fileExists('index.html')) {
//                         error('index.html file not found!')
//                     }
                    
//                     // You could add more validation here using:
//                     // - HTML validators (vnu.jar)
//                     // - Link checkers
//                 }
//             }
//         }

//         stage('Deploy Locally') {
//             steps {
//                 script {
//                     // Stop any existing server
//                     sh 'pkill -f "http-server" || true'
                    
//                     // Start new server (Node.js required)
//                     sh 'npx http-server -p 3000 . &'
                    
//                     echo 'Your site is now running at http://localhost:3000'
//                 }
//             }
//         }
//     }

//     post {
//         always {
//             // Optional: Add cleanup steps here
//             echo 'cleanup'
//         }
//         success {
//             // Optional: Add notifications here
//             echo 'Deployment succeeded!'
//         }
//         failure {
//             // Optional: Add notifications here
//             echo 'Deployment failed!'
//         }
//     }
// }
pipeline {
    agent any

    environment {
        // Set Git Bash as shell on Windows
        SHELL = 'C:\\Program Files\\Git\\bin\\bash.exe'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Venkat834/samplewebsite.git'
            }
        }

        stage('Validate HTML') {
            steps {
                script {
                    if (!fileExists('index.html')) {
                        error('❌ index.html file not found!')
                    } else {
                        echo '✅ index.html found!'
                    }
                }
            }
        }

        stage('Deploy Locally') {
            steps {
                script {
                    // Stop any existing server (optional on Windows, handled gracefully)
                    bat 'pkill -f "http-server" || true'

                    // Start HTTP server (requires Node.js + http-server module)
                    bat 'nohup npx http-server -p 3000 . > server.log 2>&1 &'

                    echo '🚀 Your site is now running at http://localhost:3000'
                }
            }
        }
    }

    post {
        always {
            echo '🧹 Performing cleanup (if any)...'
        }
        success {
            echo '✅ Deployment succeeded!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}

