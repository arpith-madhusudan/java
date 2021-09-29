pipeline{
    agent any
    stages{
        stage("git checkout"){
            steps{
                git url:"https://github.com/arpith-madhusudan/java.git",branch:"master"
            }
        }
        stage("buid"){
            steps{
                sh "/usr/share/apache-maven/bin/mvn clean package"
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy"){
            steps{
                sshagent(['tomcat']) {
                    sh """
                        scp -o StrictHostKeyChecking=no target/myweb.war ec2-user@172.31.95.66:/opt/tomcat8/webapps/
                        ssh ec2-user@172.31.95.66 /opt/tomcat8/bin/shutdown.sh
                        ssh ec2-user@172.31.95.66 /opt/tomcat8/bin/startup.sh
                      """
    
                }
            }
        }
    }

}
