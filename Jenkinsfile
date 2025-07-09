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

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Venkat834/samplewebsite.git'
            }
        }

        stage('Validate HTML') {
            steps {
                script {
                    if (fileExists('index.html')) {
                        echo '✅ index.html found!'
                    } else {
                        error('❌ index.html file not found!')
                    }
                }
            }
        }

        stage('Deploy Locally') {
            steps {
                script {
                    bat '''
                        taskkill /F /IM node.exe || echo "No running http-server to stop"
                        npx http-server -p 3000
                    '''
                    echo '✅ Your site is now running at http://localhost:3000'
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


