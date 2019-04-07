node('Build Docker'){
    def app;
    def mycfg_file=' c7edaef0-eebb-4cde-b0ed-0600830a82cd';
    currentBuild.result='SUCCESS'
    
    try{
          stage('Read Configuration file'){
         
                   configFileProvider([configFile(fileId: mycfg_file, variable: 'list')]) {
                    echo " =========== ^^^^^^^^^^^^ Reading config from pipeline script "
                    sh "cat ${env.list}"
                    echo " =========== ~~~~~~~~~~~~ ============ "

              }
          }
          
          stage('Build Image'){
          }
          
          stage('Deploy Image'){
          }
          
          stage('Cleanup'){
          }
          
      }catch(err){
          
        currentBuild.result = "FAILURE"

            mail body: "project build error is here: ${env.BUILD_URL}" ,
            from: 'info@bidcrm.com',
            replyTo: 'sjana@bidcrm.com',
            subject: 'project build failed',
            to: 'sjana@bidcrm.com'

        throw err
      }
    
}
