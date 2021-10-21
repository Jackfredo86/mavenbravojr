pipeline
{
    agent any
    stages
    {
        stage(ContinuousDownload)
        {
            steps
            {
                git 'https://github.com/Jackfredo86/mavenbravojr.git'
            }
        }
        stage(ContinuousBuild)
        {
            steps
            {
                sh 'mvn package'
            }
        }
         stage(ContinuousDeployment)
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'f011aa4f-2e7b-461e-b807-ce4fef55befd', path: '', url: 'http://172.31.99.172:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
         stage(ContinuousTesting)
        {
            steps
            {
                git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline/testing.jar'
            }
        }
         stage(ContinuousDelivery)
        {
            steps
            {
                input message: 'Waiting for approval from DM!', submitter: 'anto'
                deploy adapters: [tomcat9(credentialsId: 'f011aa4f-2e7b-461e-b807-ce4fef55befd', path: '', url: 'http://172.31.109.217:8080')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
    }
}
