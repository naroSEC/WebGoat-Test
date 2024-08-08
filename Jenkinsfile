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

		stage('SAST') {
			steps{
				script{
					def GIT_URL = env.GIT_URL
					def GET_BRANCH = env.GIT_BRANCH

					build job: 'SAST-SonarQube', parameters:[
						string(name: 'GIT_URL', value: GIT_URL),
						string(name: 'GIT_BRANCH', value: GIT_BRANCH),
						string(name: 'GIT_REPONAME', value: gitRepoName)
					]
				}
			}
		}
	}
}
