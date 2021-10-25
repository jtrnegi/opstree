# Cluster creation with ALB plus ingress controller
# opstree
creation of EKS cluster and whitelisting of Source IP via ingress

# 1) create EKS cluster via eksctl command line
> eksctl create cluster --name=attractive-gopher \
--node-type=t2.small --nodes-min=2 --nodes-max=2 \
--region=us-east-1 --zones=us-east-1a,us-east-1b,us-east-1c,us-east-1d,us-east-1f 

# 2) Create a IAM policy for ingress controller from IAM 
> use the IAM.json file and create a new policy 

# 3) Attach the new created IAM policy to the EKS worker node

# 4) Deploy RBAC and Rolebindings
> use the file rbac.yaml to create the same
> kubectl apply -f rbac.yaml

# 5) Create the ALB and ingress controller
>use the alb-ingress-controller.yaml
>kubectl apply -f alb-ingress-controller.yaml


# Deployment of sample application
# 1) Create a namespace 2048-game
>kubectl apply -f namespace.yaml

# 2) Create a deployment of sample game "2048" with 5 replicas
>kubectl apply -f deployment.yaml

# 3) Create a service to expose the backend deployment 
>kubectl apply -f service.yaml

# 4) Deploy an an ingress
>kubectl apply -f ingress.yaml

------------------------------------------------------------------------------------------------------------------------------------------------------------------

# For whitelisting of source IP
> We need to add the parameter "alb.ingress.kubernetes.io/inbound-cidrs: SourceIP/32" under the annotations parts inside the ingress.yaml for the whitelisting of source ip 

