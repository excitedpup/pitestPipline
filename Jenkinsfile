pipeline {
    agent any
    
    tools {
        // Install the Maven version configured as "MAVEN" under Global Tool Configurations and add it to the path.
        maven "MAVEN"
    }
    
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                // **link needs to be updated**
                git branch: 'main', url: 'https://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@github.com/deemsa64/Junit-Demo.git'
                
                // Set a maven project workspace with Pit as well as Git Commands
                // ***ws path may need to be updated*** remove this comment when updated
                ws('/var/lib/jenkins/workspace/PitPipeline2/junit-demo/') {
                    // compile the tests
                    sh  "mvn test-compile org.pitest:pitest-maven:mutationCoverage"
                    // Create a PIT mutation report using the PIT Report plugin.
                    pitmutation()
                    
                    // Creates link to the Pit Report
                    publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '', reportFiles: '**/target/pit-reports/**/index.html', reportName: 'HTML Report', reportTitles: ''])
                    //bat 'git add .' // Adds all changes made by this jenkins pipeline (primarily PIT reports
                                      // to the git repo)
                    //bat 'git commit' 
                    //bat 'git push'
                    //test using freestyle project push plugin (not availible in pipeline)
                    //think about adding in mvn clean install later if we want to clean up the reports in github repo
                    //with credentials pipeline syntax may be useful for git add, push, pull?
                }
                
            }
        }
    }
}
