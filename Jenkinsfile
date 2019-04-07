node{
    def app;
    def config_id='c7edaef0-eebb-4cde-b0ed-0600830a82cd';
    def buildInfo2;
    currentBuild.result='SUCCESS'
    
    try{
          stage('Read Configuration file'){
         
                configFileProvider([configFile(fileId: config_id, variable: 'PACKER_OPTIONS')]) {
                echo " =========== ^^^^^^^^^^^^ Reading config from pipeline script "
                //sh "cat ${env.PACKER_OPTIONS} >x.txt"
                    
                //buildInfo2 = new JsonBuilder(load("${env.PACKER_OPTIONS}"))
                 //echo " ${env.PACKER_OPTIONS}"
                //buildInfo2=load("./x.txt")
                    
                //echo "Test:" +buildInfo2.toString()

           
                }
              
              git "https://github.com/cloudtestsoftware/Login_Docker_alphine.git"
          }
          
          stage('Build Image'){
              app =docker.build('bidcrm/test:Test-${BUILD_NUMBER}')
          }
          
          stage('Test Image'){
              app.inside{
                  echo "Test Passed"
              
              }
          }
          
          stage('Push Image'){
              docker.withRegistry('https://cloud.docker.com/repository/docker/bidcrm/test','DockerRepo')
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
