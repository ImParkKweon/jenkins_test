pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // GitHub 저장소를 클론합니다.
                git 'https://github.com/ImParkKweon/product.git'
            }
        }
        
        stage('Modify Code') {
            steps {
                // 코드 수정 작업을 수행합니다.
                script {
                    def modifiedCode = readFile('backend/deploy.yaml')
                    // 여기에서 modifiedCode를 원하는 방식으로 수정합니다.
                    // 예를 들면, 문자열 치환, 코드 조작 등
                    // 수정된 코드를 저장합니다.
                    writeFile(file: 'backend/deploy_mod.yaml', text: modifiedCode)
                }
            }
        }
        
        stage('Commit and Push Changes') {
            steps {
                // 수정된 코드를 다시 커밋하고 푸시합니다.
                script {
                    def commitMessage = "이미지 태그 최신화"
                    
                    // GitHub 계정 로그인 정보를 설정합니다.
                    withCredentials([usernamePassword(credentialsId: 'github_access_token', passwordVariable: 'GITHUB_TOKEN', usernameVariable: 'GITHUB_USERNAME')]) {
                        // Git 커맨드를 사용하여 변경 사항을 커밋하고 푸시합니다.
                        sh "git add backend/deploy_mod.yaml"
                        sh "git commit -m '${commitMessage}'"
                        sh "git push"
                    }
                }
            }
        }
    }
}
