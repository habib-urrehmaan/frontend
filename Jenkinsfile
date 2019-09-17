pipeline 
{
  environment 
  {
    registry = "habiburrehman344/frontend"
    registryCredential = 'docker-credentials'
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
          echo 'Application was built'
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

    stage('Initialize Minikube')
    {
      steps
      {
        script
        {
          sh "minikube start"
        }
      }
    }

    stage('Update Deployment')
    {
      steps
      {
        script
        {
          sh "kubectl apply -f frontend.yaml"
        }
      }
    }
  }
}