Here is the steps of project with related commands

1-Creating namespace:
	kubectl create namespace limited-ns

2-Creating a serviceaccount for user:
	kubectl create serviceaccount limited-user -n limited-ns

3-Defining limited role: 
	limited-role.yaml

4-Apply these roles:
	kubectl apply -f limited-role.yaml

5-In order to assign above roles to the serviceaccount, we should define rolebinding:
	limited-rolebinding.yaml
	kubectl apply -f limited-rolebinding.yaml 

6-In order to prevent overuswed of resources by pods, we defined ResourceQuota  and LimitRange :
	kubectl apply -f resource-quota.yaml
	kubectl apply -f limit-range.yaml

7- In order to increase network security, we network policy on all traffics except DNS:
	kubectl apply -f deny-all.yaml
	kubectl apply -f allow-dns-egress.yaml

8-Create kubeconfig for user to access to have cluster:
	SECRET_NAME=$(kubectl -n limited-ns get sa limited-user -o jsonpath="{.secrets[0].name}")
	USER_TOKEN=$(kubectl -n limited-ns get secret $SECRET_NAME -o jsonpath="{.data.token}" | base64 --decode)
	CLUSTER_NAME=$(kubectl config view --minify -o jsonpath='{.clusters[0].name}')
	CLUSTER_SERVER=$(kubectl config view --minify -o jsonpath='{.clusters[0].cluster.server}')
	CLUSTER_CA=$(kubectl config view --minify --raw -o jsonpath='{.clusters[0].cluster.certificate-authority-data}')


 
