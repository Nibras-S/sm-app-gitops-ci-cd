
# Install Argo CD
# Install Argo CD using manifests
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
# Access the Argo CD UI (Loadbalancer service)
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
# Access the Argo CD UI (Loadbalancer service) -For Windows
kubectl patch svc argocd-server -n argocd -p '{\"spec\": {\"type\": \"LoadBalancer\"}}' 
# Get the Loadbalancer service IP
kubectl get svc argocd-server -n

# To get password
kubectl get secrets -n argocd
kubectl edit secret argocd-initial-initial-admin-secret -n argocd       step1
kubectl get secret argocd-initial-admin-secret -o jsonpath='{.data.password}' -n argocd     step 2

# Decode the password
# For Git Bash:
echo <paste-base64-password-here> | base64 --decode

# For Windows PowerShell:
[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String("<paste-base64-password-here>"))

# Login to Argo CD at http://<LoadBalancer-IP>
# Username: admin
# Password: (decoded from above)
