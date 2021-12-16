
pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/mbongowo/maven.git' 
                    }
                    catch(Exception e1)
                    {
                       mail bcc: '', body: 'Jenkins is unable to download the dev code from github', cc: '', from: '', replyTo: '', subject: 'Download Failed', to: 'git.team@gmail.com'
                       exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                script
                {
                    try
                    {
                           sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code', cc: '', from: '', replyTo: '', subject: 'Buid Failed', to: 'developers.team@gmail.com'
                        exit(1)
                    }
                }
             
            }
        }
        stage('ContinuousDeployment')
        {
            steps
            {
                script
                {
                    try
                    {
                      deploy adapters: [tomcat9(credentialsId: 'b86a9399-7a2b-467b-acd7-5e2443d4d82f', path: '', url: 'http://172.31.91.36:8080')], contextPath: 'testapp', war: '**/*.war'  
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy artifact into tomcat on the QAServers', cc: '', from: '', replyTo: '', subject: 'Deployment Failed', to: 'middleware.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipelinewithExceptionhandling1/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium test scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
               
            }
        }
         stage('ContinuousDelivery')
        {
            steps
            {
                script
                {
                    try
                    {
                              deploy adapters: [tomcat9(credentialsId: 'b86a9399-7a2b-467b-acd7-5e2443d4d82f', path: '', url: 'http://172.31.86.130:8080')], contextPath: 'prodapp', war: '**/*.war'

                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodservers', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
                    }
                }
              
            }
        }
        
    }
}

