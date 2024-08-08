#!groovy
@Library('jenkins-lib') _

pipeline {
	agent any

	environment {
		gitRepoName = getGitRepoName()
	}

	stages{
		stage('Checkout SCM') {
			steps {
				echo 'Checkout SCM!'
				// Jenkins 프로젝트에 설정된 Repository로 부터 현재 브랜치의 소스코드를 가져오는데 사용한다.
				checkout scm
			}
		}

		stage('Build') {
			steps {
				script {
					sh "chmod u+x ./mvnw"
                    sh "./mvnw clean package"
				}
			}
		}

		stage('Deploy') {
			steps {
				echo 'Deploy is not yet implemented!'
			}
		}

		stage('SonarQube Start!') {
			steps{
				script{
					def URL = env.GIT_URL
					def BRANCH = env.GIT_BRANCH

					build job: 'security_job', parameters:[
						string(name: 'GITURL', value: URL),
						string(name: 'BRANCH', value: BRANCH),
						string(name: 'REPO', value: REPO_NAME)
					]
				}
			}
		}
	}
}
