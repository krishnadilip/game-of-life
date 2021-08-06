pipeline 
{
  agent{ label 'GOL' }
  triggers{
      cron ('H * * * *')
      pollSCM('* * * * *')
  }
  parameters{
      string(name: 'branch', defaultValue: 'master', description: 'branch to build')
  }
  environment{
      main = 'frompipeline'
  }
  }
  stages
  {
      stage ('scm')
      {
          steps
          {
             // sh 'GIT url is ${GIT_URL}'
              mail subject: "build started on branch ${env.GIT_BRANCH} with it build id ${env.BUILD_ID}", to: 'dilip.abcdefg@gmail.com', from: 'dilip@jenkins.in'
              git branch "${params.branch}", url: 'https://github.com/krishnadilip/game-of-life.git'
              input 'continue to next stage? '
              //input message: 'continue to next stage? ', submitter: 'krishna'
                }
      }
      stage ('build')
      {
            environment{
                instage = 'within stage'
            }
            steps{
                mail subject: 'build started successfully'+env.BUILD_ID, to: 'dilip.abcdefg@gmail.com', from: 'dilip@jenkins.in', body: 'empty body'
                echo env.GIT_URL
                echo env.instage 
                echo env.main 
                timeout(time:10, unit:'MINUTES' )
                sh 'mvn package'  
            } 
      }
      }
  }
  post{
  success{
    archive '**/gameoflife.war'
    junit '**/TEST_*.xml'
    mail subject: 'build completed successfully'+env.BUILD_ID, to: 'dilip.abcdefg@gmail.com', from: 'dilip@jenkins.in', body: 'empty body'
     }
  failure{
      mail subject: 'build is failed'+env.BUILD_URL, to: 'dilip.abcdefg@gmail.com', from: 'dilip@jenkins.in', body: 'empty body'
  }
  }
}