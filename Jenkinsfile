@Library('gest-global-library')_
node(label: 'mule-builder') {
  def map = [:]
  
  	/* Add main-vendor-credentials and develop-vendor-credentials in Jenkins->Credentials. 
  		Credential values from Jenkins is then set to variable VENDOR_USER and VENDOR_USER which is
  		then used in pom.xml to set vendor.username and vendor.password
  		which is then used within Mule app as ${vendor.username} */
  		
  withCredentials([
    usernamePassword(credentialsId: "${BRANCH_NAME}-develop-cdp-consumer-credentials", usernameVariable: "CDP_KEY", passwordVariable: "CDP_SECRET"),
    usernamePassword(credentialsId: "${BRANCH_NAME}-develop-cdp-access-credentials", usernameVariable: "CDP_USER", passwordVariable: "CDP_PASS")
  ]) {
  
  	/* -X for Maven debug mode */
  	def mvnParams = "-Denv.CDP_KEY=${CDP_KEY} 
  	-Denv.CDP_SECRET=${CDP_SECRET}
  	-Denv.CDP_USER=${CDP_USER}
  	-Denv.CDP_PASS=${CDP_PASS}"
    map.put('mvnParams', mvnParams)
    map.put('SLAVE_NODE_NAME', "mule-builder")
    map.put('MULE_RUNTIME_VERSION', "4.4.0")
    map.put('WORKER_TYPE',"Micro")
    
    
    /* Set your Mule app name here. Use format: bg-sys_or_pro_or_exp-myappname-api-vN" */    
    map.put('APP_NAME', "rcg-salesforce-cdp-sapi")
    
    /* Set BUSINESS_GROUP_ID from your group in 1Platform 
    	BUSINESS_GROUP_ID is used in pom.xml to set businessGroupId */
    map.put('BUSINESS_GROUP_ID', "d232aa42-ae6f-4469-b026-bc9377aadc4f")
    
    buildPipeline(map)
  }
}