kubectl create clusterrole sa-health-check \
          --verb=get --verb=list --verb=create --verb=update  \
          --resource=secret \
          --namespace=default

kubectl create clusterrolebinding sa-health-check \
          --role=role-full-access-to-secrets \
          --serviceaccount=default:sa-health-check\
          --namespace=default

Check the  permission is working:
 kubectl get secret --namespace=default  --as=system:serviceaccount:default:sa-health-check
 
helm install test-gateway . --set namespace=default

helm upgrade --install test-gateway . --set namespace=default

