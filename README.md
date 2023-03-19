## SPCN04
## Kubernetes

## Wakatime
https://wakatime.com/@spcn04/projects/nqgwrowcuf

## 1. Install Kubectl
   - Ref 
    - https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

   - download Kubectl.exe to path want

      ```
      curl.exe -LO "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"
      ``` 
   - Add Path to environment variable
      - Search environment
  
        ![image](https://user-images.githubusercontent.com/119097663/224904080-a7de4fcd-c43d-4760-b483-0734aaeca796.png)


      - Click Environment Variables...

        ![image](https://user-images.githubusercontent.com/119097663/224904504-ac4bb0b8-4a35-4ddd-87c0-d0f665c86d04.png)

       - Select Path Click Edit

        ![image](https://user-images.githubusercontent.com/119097663/224904590-64c1e452-efae-41f9-861e-409f9e9b9e78.png)

       - Click New
        
        ![image](https://user-images.githubusercontent.com/119097663/224904653-d6231336-cf6a-4280-bdba-2e72043c5a5c.png)

      - Add Path that have kubectl.exe
      - Click OK
  
      - Test Kubectl enable in command
      ```ruby
      kubectl version --client
      ```

## 2. Install minikube
   - Ref
    - https://minikube.sigs.k8s.io/docs/start/

      - download minikube.exe

      ```ruby
      New-Item -Path 'c:<path want to install>' -Name 'minikube' -ItemType Directory -Force #create folder minikube
      Invoke-WebRequest -OutFile 'c:<path want to install>\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing #download install to path
      ```

      - Add Path to environment variable
      ```ruby
      $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
      if ($oldPath.Split(';') -inotcontains 'C:<path folder minikube.exe>'){ `
      [Environment]::SetEnvironmentVariable('Path', $('{0};C:<path folder minikube.exe>' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
      }
      ```
   - Restart Terminal

## 3. Install Docker Desktop
   - Ref
    - https://docs.docker.com/desktop/install/windows-install/

## Test minikube start
1. Start a cluster using the docker driver
   ```ruby
   minikube start --driver=docker
   ```
   ![image](https://user-images.githubusercontent.com/115150753/226189890-047f8292-231e-4671-9bea-9c8808c609ff.png)

2. Run with open dashboard
   ```ruby
   minikube dashboard
   ```
   ![image](https://user-images.githubusercontent.com/115150753/226189931-6ba8aa0b-0172-4792-892f-5da1d9d2aa53.png)

3. Test services
   ```ruby
   minikube service hello-minikube
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907641-f32599e8-afd0-4a9e-8bf5-f8a59c476752.png)

4. Test Stop minikube
   ```ruby
   minikube pause
   ```
   ![image](https://user-images.githubusercontent.com/115150753/226190030-9dfcdcdf-28ea-4597-9e3a-b1107e06b950.png)

## 4. Install traefik
1. Install Traefik Resource Definitions
   ```ruby
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
   ```
    ![image](https://user-images.githubusercontent.com/115150753/226190072-38893ffc-5660-487a-ba9b-ccc286b3f850.png)

2. Install RBAC for Traefik
   ```ruby
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
   ```

3. Install Traefik Helmchart
   ```ruby
   helm repo add traefik https://traefik.github.io/charts 
   helm repo update 
   helm install traefik traefik/traefik 
   ```

4. Verify service is running
   ```ruby
   kubectl get svc -l app.kubernetes.io/name=traefik
   kubectl get po -l app.kubernetes.io/name=traefik
   ```

5. copy user in dashboard-secret place it at user in traefik-dashboard



6. Deploy
   ```ruby
   kubectl apply -f . 
   ```
   ![image](https://user-images.githubusercontent.com/115150753/226190125-8e058b95-f583-4900-be6b-d5b3f09fb129.png)

## Result

## 1. dashboard

![image](https://user-images.githubusercontent.com/115150753/226189931-6ba8aa0b-0172-4792-892f-5da1d9d2aa53.png)

## 2. https://traefik.spcn04.local/dashboard/#/http/routers

![image](https://user-images.githubusercontent.com/115150753/226190166-87f3dc3b-40c2-4e3f-a4ee-11834c667388.png)

## 3. http://web.spcn04.local/

![image](https://user-images.githubusercontent.com/115150753/226190214-13485993-00af-44d6-804e-aa72ca11ab6d.png)

