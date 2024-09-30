pipeline
{
    agent any
    stages
    {
        stage('continuousdownload')
        {
            steps
            {
             git 'https://github.com/Ashok-Cherukuri/maven.git'    
            }
        }
        stage('continuousbuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('continuousDeploy')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: '42cca5b6-494f-4fda-b243-938b9a4f49e9', path: '', url: 'http://172.31.1.226:8080')], contextPath: 'Qtest', war: '**/*.war'
            }
        }
        stage('continuoustesting')
        {
            steps
            {
                git 'https://github.com/Ashok-Cherukuri/FunctionalTesting.git'
                sh 'java -jar  /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('continuousdelivery')
        {
            steps
            {
                deploy adapters: [tomcat9(credentialsId: 'f12c397f-7230-46c5-baa9-3a256e8aa204', path: '', url: 'http://172.31.42.60:8080')], contextPath: 'Ptest', war: '**/*.war'
            }
        }
    }
}
