Create Helm charts for application:
Organize application into Helm charts (e.g.Chart.yaml, values.yaml, deployment.yaml, service.yaml,templates).

(1).Installation of helm:-
curl https://get.helm.sh/helm-v3.14.0-linux-amd64.tar.gz
curl -O https://get.helm.sh/helm-v3.14.0-linux-amd64.tar.gz
tar -xzf helm-v3.14.0-linux-amd64.tar.gz

helm binary move it to its desired destination
 mv helm /bin/

(2). Install AWS Load Balancer Controller:

helm repo add eks https://aws.github.io/eks-charts
helm repo update

helm install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=pc-eks \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller 

kubectl get deployment -n kube-system aws-load-balancer-controller

kubectl create namespace nlb-sample-app

(3). Deploy the application with Helm:

cd nlb-sample-app
helm create helm-myntra
helm install myntra-basic helm-myntra/ -n nlb-sample-app

Check kubectl  pod and service status:
kubectl get svc

kubectl get pod

kubectl get deployment

To uninstall:
helm uninstall myntra-basic


(4). Expose the application with NLB:
Ensure that Helm charts create a Service of type LoadBalancer.
The AWS Load Balancer Controller should automatically create an NLB for Service.

(5). Verify the deployment:
kubectl get pods  
kubectl get svc  #To check the status of deployment.
Access application using the NLB URL.
This is a high-level overview, and may need to customize it based on specific application, requirements and architecture.
