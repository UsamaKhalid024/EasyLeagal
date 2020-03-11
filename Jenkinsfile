#!groovy
import groovy.json.JsonSlurperClassic
node {

    def BUILD_NUMBER=env.BUILD_NUMBER
    def RUN_ARTIFACT_DIR="tests/${BUILD_NUMBER}"
    def SFDC_USERNAME

    def HUB_ORG="usama@ioptime.com"
	def jwt_key_file="usama@ioptime.com"
    def SFDC_HOST = "https://login.salesforce.com/"
    def JWT_KEY_CRED_ID = "8ccb15ac-8250-4735-95c8-d560b7b3ff9a"
    def CONNECTED_APP_CONSUMER_KEY = "3MVG9G9pzCUSkzZvUX.xGKvFpuwjGYquEFgY6OX6UELIAvmQDx6YBJ6NFy67CsCZJlJvq7V5hy9W6RgiuwDEt"

    println 'KEY IS' 
    println JWT_KEY_CRED_ID
    println HUB_ORG
    println SFDC_HOST
    println CONNECTED_APP_CONSUMER_KEY
    def toolbelt = tool 'toolbelt'

    stage('checkout source') {
        // when running in multi-branch job, one must issue this command
        checkout scm
    }

    withCredentials([file(credentialsId: JWT_KEY_CRED_ID, variable: 'jwt_key_file')]) {
        stage('Deploye Code') {
            if (isUnix()) {
                rc = sh returnStatus: true, script: "${toolbelt} force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile ${jwt_key_file} --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
            }else{
                 
				 rc = bat returnStatus: true, script: "${toolbelt} force:auth:jwt:grant --clientid ${CONNECTED_APP_CONSUMER_KEY} --username ${HUB_ORG} --jwtkeyfile ${jwt_key_file} --setdefaultdevhubusername --instanceurl ${SFDC_HOST}"
   `
   
            }
			println rc
            if (rc != 0) { error 'hub org authorization failed' }

			println rc
			
			

			
        }
    }
}
