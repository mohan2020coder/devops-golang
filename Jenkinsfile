pipeline {
    agent any

   tools {
       go 'go1.22.4'
    }

    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN') // Reference Jenkins credential ID
        SUDO_PASSWORD = credentials('SUDO_PASS_ID')
    }

    stages {
        stage('Unit Test') {
            steps {
                script {
                    sh 'go mod init github.com/mohan2020coder/devops-golang'
                    sh 'go test'
                }
            }
        }

        stage('Coverage Report') {
            steps {
                script {
                    sh 'go test -coverprofile=coverage.out'
                    sh 'go tool cover -html=coverage.out -o coverage.html'
                }
                archiveArtifacts 'coverage.html'
            }
        }

        stage('Run SonarQube Analysis') {
            steps {
                script {
                        sh '/usr/local/sonar/bin/sonar-scanner -X -Dsonar.organization=moniorg -Dsonar.projectKey=moniorg_devops-golang -Dsonar.sources=. -Dsonar.host.url=https://sonarcloud.io'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Adjust these commands based on how you build and upload your Go application to Nexus
                    sh 'go build -o main .'
                    // sh 'curl -u username:password -X PUT --upload-file your-app https://nexus.example.com/repository/your-repo/your-app/1.0.0/your-app-1.0.0'
                }
                archiveArtifacts 'main'
            }
        }

        stage('Build Docker Image') {
           steps {
               script {
                   sh 'docker build -t monihub/hellogo .'
               }
           }
       }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DOCKER_REGISTRY_CREDENTIALS_ID', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh '''
                            echo "${DOCKER_PASSWORD}" | docker login --username "${DOCKER_USERNAME}" --password-stdin
                            docker push monihub/hellogo
                        '''
                    }
                }
            }
        }

       // stage('Terraform Apply') {
       //      environment {
       //          AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
       //          AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
       //      }
       //      steps {
       //          script {
       //              sh '''
       //                  export AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
       //                  export AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
       //                  cd ./terraform
       //                  terraform init
       //                  terraform apply -auto-approve
       //              '''
       //          }
       //      }
       //  }

        // stage('Run Ansible Playbook') {
        //     steps {
        //         script {
        //             sh '''
        //                 ansible-playbook ansible/deploy-container.yaml
        //             '''
        //         }
        //     }
        // }
      
        stage('Deploy Container') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'SUDO_PASS_ID', variable: 'SUDO_PASSWORD')]) {
                        sh 'ansible-playbook ansible/deploy-container.yaml --extra-vars "ansible_become_pass=$SUDO_PASSWORD"'
                    }
                }
            }
        }
  
    }

    post {
        always {
            cleanWs()
        }
    }
}
// pipeline {
//     agent any

//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout scm
//             }
//         }

//         stage('Initialize Go Module') {
//             steps {
//                 script {
//                     if (!fileExists('go.mod')) {
//                         sh 'go mod init https://github.com/mohan2020coder/devops-golang'
//                     }
//                 }
//             }
//         }

//         stage('Get Dependencies') {
//             steps {
//                 sh 'go get -u ./...'
//             }
//         }

//         stage('Build') {
//             steps {
//                 sh 'go build -v ./...'
//             }
//         }

//         stage('Test') {
//             steps {
//                 sh 'go test -v ./...'
//             }
//         }
//     }
// }
