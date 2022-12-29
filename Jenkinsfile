#!groovy

node {

    def SF_CONSUMER_KEY_DEV = 3MVG9n_HvETGhr3BxaUyKW0eA.LmfJN4mFPqjXeQFtQbda7DajbisyQcOV3B2hoXTVPekHwtyOMw6UcH2nQjb
    def SF_USERNAME_DEV = hvbhardwaj@sexy.com
    def SF_CONSUMER_KEY_TEST=3MVG9n_HvETGhr3BaZdVEARq2E0Xdcs8WOzo8yLqeYnz8iYmUpUpTd5fBSeuRW98PTnRpXZVu4GifIbeAu98D
    def SF_USERNAME_TEST= vaibhav.srivastavaknp-gha1@force.com
    def SERVER_KEY_CREDENTIALS_ID=9f369130-6f60-4cc7-8576-4b84f044e968
    def SF_INSTANCE_URL = https://login.salesforce.com

    def toolbelt = tool 'toolbelt'


    // -------------------------------------------------------------------------
    // Check out code from source control.
    // -------------------------------------------------------------------------

    stage('checkout source') {
        checkout scm
    }


    // -------------------------------------------------------------------------
    // Run all the enclosed stages with access to the Salesforce
    // JWT key credentials.
    // -------------------------------------------------------------------------

	
	    withCredentials([file(credentialsId: SERVER_KEY_CREDENTIALS_ID, variable: 'server_key_file')]) {
		// -------------------------------------------------------------------------
		// Authenticate to Salesforce using the server key.
		// -------------------------------------------------------------------------

		stage('Authorize to Salesforce') {
			rc = command "${toolbelt}/sfdx auth:jwt:grant --instanceurl ${SF_INSTANCE_URL} --clientid ${SF_CONSUMER_KEY_DEV} --jwtkeyfile ${server_key_file} --username ${SF_USERNAME_DEV} --setalias DEV
		    if (rc != 0) {
			error 'Salesforce org authorization failed.'
		    }
		}

        	stage('Authorize to Salesforce') {
			rc = command "${toolbelt}/sfdx auth:jwt:grant --instanceurl ${SF_INSTANCE_URL} --clientid ${SF_CONSUMER_KEY_TEST} --jwtkeyfile ${server_key_file} --username ${SF_USERNAME_TEST} --setalias TEST
		    if (rc != 0) {
			error 'Salesforce org authorization failed.'
		    }
		}

        }
}
def command(script) {
    if (isUnix()) {
        return sh(returnStatus: true, script: script);
    } else {
		return bat(returnStatus: true, script: script);
    }
}