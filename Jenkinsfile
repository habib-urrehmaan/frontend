pipeline 
{
  environment 
  {
    registry = "habiburrehman344/frontend"
    registryCredential = 'DockerHub'
  }
  
  agent any
  // tools {nodejs "node"}

  stages 
  {
    stage('Pulling') 
    {
      steps 
      {
        sh "git pull https://github.com/habiburrehman012/frontend.git"
      }
    }



    stage('Building Application')
    {
      steps 
      {
          sh 'npm install'
      }
    }

    stage('Building image') {
      steps
      {
        sh 'docker build -t habiburrehman344/frontend:latest .'
      }
    }

    stage('Push image') 
    {
      steps 
      {
        script 
        {
          docker.withRegistry( '', registryCredential ) 
          {
            sh 'docker push habiburrehman344/frontend:latest'
          }
        }
      }
    }

    stage('Apply Development') {
      steps
      {
        sh 'kubectl scale --replicas=0 deployment python-frontend'
        sh 'kubectl scale --replicas=1 deployment python-frontend'
      }
    }
  }
}