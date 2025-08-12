

# Follow this video to be a ArgoCD Boss
https://youtu.be/JLrR9RV9AFA


# Installing latest/stable version of ArgoCD
- [x] kubectl create namespace argocd
- [x] kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

- [x] kubectl get all -n argocd

# Forward Ports
- [x] kubectl get services -n argocd
- [x] kubectl port-forward service/argocd-server -n argocd 8080:443


# Get Credentials
- [x] kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d


# Install ArgoCD CLI / Login via CLI
- [x] brew install argocd
- [x] kubectl port-forward svc/argocd-server -n argocd 8080:443
- [x] argocd login 127.0.0.1:8080

# Verify running Pods and Services

# kubectl get all -n dev
NAME                             READY   STATUS    RESTARTS   AGE
- [x] NAME                             READY   STATUS    RESTARTS   AGE
- [x] pod/myhelmapp-7b5fdcd7b5-2p5s4   1/1     Running   0          2m26s
- [x] pod/myhelmapp-7b5fdcd7b5-dtlr7   1/1     Running   0          2m26s
- [x] pod/myhelmapp-7b5fdcd7b5-mrl9z   1/1     Running   0          2m26s
- [x] pod/myhelmapp-7b5fdcd7b5-tp7pc   1/1     Running   0          2m26s
- [x] pod/myhelmapp-7b5fdcd7b5-zspwp   1/1     Running   0          2m26s

NAME                TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/myhelmapp   NodePort   10.101.254.222   <none>        80:31167/TCP   2m26s

NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/myhelmapp   5/5     5            5           2m27s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/myhelmapp-7b5fdcd7b5   5         5         5       2m27s

# PORT FORWARD TO service/myhelmapp
- [x] kubectl port-forward service/myhelmapp 8888:80 -n dev

# Creating an Application using ArgoCD CLI:
- [x] Step 1 - kubectl create namespace prod 
```

argocd app create webapp-kustomize-prod \
--repo https://github.com/Nzastudios/argocd.git \
--path kustom-webapp/overlays/prod --dest-server https://kubernetes.default.svc \
--dest-namespace prod
```

# Command Cheat sheet

# Checking out of sync
- [x] argocd app diff webapp-kustomize-prod

# Sync the application if a change was made in Repository ( SYNC Set to Manual )
- [x] argocd app sync argocd/webapp-kustomize-prod

# Confirm the pods reflect the changes of the Sync
- [x] kubectl get all -n prod

# Get Details of argo CD Application
- [x] argocd get argocd/webapp-kustomize-prod

# Get Logs of argo CD Application
- [x] argocd logs argocd/webapp-kustomize-prod


# How to rollback
- [x] argocd app history webapp-kustomize-prod
- [x] argocd app rollback webapp-kustomize-prod revision_number
- [x] argocd app rollback webapp-kustomize-prod 0

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





