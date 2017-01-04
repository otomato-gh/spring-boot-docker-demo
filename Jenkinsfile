node{
        stage ('Clone sources')
        {
         
            // Get some code from git 
            checkout scm 
            // checkout scm will replace below git command 
            // git credentialsId: '131951aa-6322-41d1-8e3c-724612129f4b', url: 'git@illin5226.corp.amdocs.com:PCI_CloudLab_repo'
 
        
        }
        // Run maven
        stage ('Build app artifcat')
        {
            echo 'Build'
            withEnv(["PATH+MAVEN=${tool 'maven3.3.9'}/bin"]) {
                sh 'cd spring-boot-demo; mvn -s ../settings.xml clean test install'
            }
        }
        // Build Docker image(s)
        stage ('Build Docker image')
        {
            // sh "cd demos/oms_microservice/spring-boot-demo; sudo docker build ."
            echo 'Docker Build'
            withEnv(["PATH+MAVEN=${tool 'maven3.3.9'}/bin"]) {
                sh 'cd spring-boot-demo; mvn -s ../settings.xml package fabric8:build'
           }
        }
	
        stage ('Upload to Nexus')
        {
           echo 'Image upload'
           withEnv(["PATH+MAVEN=${tool 'maven3.3.9'}/bin"]) {
                sh 'cd spring-boot-demo; mvn -s ../settings.xml -Ddocker.registry=illin5225:5000 fabric8:push'
           }
        }

        
        stage ('Deploy to Kubernetes')
        {
           echo 'deploy'
        }
    
}
