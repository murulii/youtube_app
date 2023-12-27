# Argocd 

helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
helm install argocd argo/argo-cd


To get access Argocd GUI

kubectl port-forward svc/argocd-server 8080:443
kubectl edit service/argocd-server    ##edit argocd server to NodePort /Loadbalancer

## Install ArgoCD CLI in Cloud Shell (GCP)

```
wget https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64 -O ~/argocd
chmod +x ~/argocd
mkdir -p ~/bin
mv ~/argocd ~/bin/
echo 'export PATH=$HOME/bin:$PATH' >> ~/.bashrc
source ~/.bashrc

//login to argocd to add k8s to argocd //ip of argocd username and password
argocd login 34.171.45.65:80 --username admin

```
## Add k8s to Argocd 
```
kubectl config get-contexts

argocd cluster add gke_kubernetes-405017_us-central1-a_my-first-cluster-1 --name mycluster // replace mycluster

argocd cluster list

```
--------------------------------------------------------------------------------------------------------------------


# Monitoring

```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

helm repo add stable https://charts.helm.sh/stable
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
kubectl create namespace prometheus
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
kubectl edit svc stable-grafana -n prometheus
15661

```

-------------------------------------------------------------------------------------------------------------------
# Splunk installation (<splunk-public-ip:8000>)

```
wget -O splunk-9.1.1-64e843ea36b1-linux-2.6-amd64.deb "https://download.splunk.com/products/splunk/releases/9.1.1/linux/splunk-9.1.1-64e843ea36b1-linux-2.6-amd64.deb"

sudo dpkg -i splunk-9.1.1-64e843ea36b1-linux-2.6-amd64.deb

sudo /opt/splunk/bin/splunk enable boot-start
sudo /opt/splunk/bin/splunk start
```

-------------------------------------------------------------------------------------------------------------------
# Trivy Installation

```
sudo apt-get install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy -y
```
--------------------------------------------------------------------------------------------------------------------

