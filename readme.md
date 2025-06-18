

# Follow this video to be a ArgoCD Boss
https://youtu.be/JLrR9RV9AFA


# Installing latest/stable version of ArgoCD
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
## kubectl get all -n argocd

### Forward Ports
```
kubectl get services -n argocd
kubectl port-forward service/argocd-server -n argocd 8080:443
```

### Get Credentials
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

# Install ArgoCD CLI / Login via CLI
```
brew install argocd
kubectl port-forward svc/argocd-server -n argocd 8080:443
argocd login 127.0.0.1:8080
```

# Post creation of New webapp in ARGO CD called helm-webapp-dev
# verify apps service/myhelmapp is running along with the 5 pod replicaset

# kubectl get all -n dev
NAME                             READY   STATUS    RESTARTS   AGE
pod/myhelmapp-7b5fdcd7b5-2p5s4   1/1     Running   0          2m26s
pod/myhelmapp-7b5fdcd7b5-dtlr7   1/1     Running   0          2m26s
pod/myhelmapp-7b5fdcd7b5-mrl9z   1/1     Running   0          2m26s
pod/myhelmapp-7b5fdcd7b5-tp7pc   1/1     Running   0          2m26s
pod/myhelmapp-7b5fdcd7b5-zspwp   1/1     Running   0          2m26s

NAME                TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/myhelmapp   NodePort   10.101.254.222   <none>        80:31167/TCP   2m26s

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/myhelmapp   5/5     5            5           2m27s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/myhelmapp-7b5fdcd7b5   5         5         5       2m27s

### PORT FORWARD TO service/myhelmapp
### kubectl port-forward service/myhelmapp 8888:80 -n dev

# Creating an Application using ArgoCD CLI:
```
argocd app create webapp-kustom-prod \
--repo https://github.com/devopsjourney1/argo-examples.git \
--path kustom-webapp/overlays/prod --dest-server https://kubernetes.default.svc \
--dest-namespace prod
```

# Command Cheat sheet
```
argocd app create #Create a new Argo CD application.
argocd app list #List all applications in Argo CD.
argocd app logs <appname> #Get the application’s log output.
argocd app get <appname> #Get information about an Argo CD application.
argocd app diff <appname> #Compare the application’s configuration to its source repository.
argocd app sync <appname> #Synchronize the application with its source repository.
argocd app history <appname> #Get information about an Argo CD application.
argocd app rollback <appname> #Rollback to a previous version
argocd app set <appname> #Set the application’s configuration.
argocd app delete <appname> #Delete an Argo CD application.
```





