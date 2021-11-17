# k8project
Advanced Devops project by Ohad Kless, HP Indigo

Did the following:
1. Installed Jenkins:
	helm repo add jenkinsrepo https://charts.jenkins.io
	helm install jenkins jenkinsrepo/jenkins --set controller.serviceType=NodePort
	minikube service jenkins
2. Cloned https://github.com/avielb/rmqp-example
3. Converted docker-compose yaml to Helm chart with tool kompose:
	Install kompose:
		curl -L https://github.com/kubernetes/kompose/releases/download/v1.24.0/kompose-windows-amd64.exe -o kompose.exe
		chmod +x kompose
		Copy compose file to location of kompose
		cd /c/GitWS/k8training/rmqp-example
		/c/temp/kompose.exe convert -c
			WARN Service "consumer" won't be created because 'ports' is not specified
			WARN Service "producer" won't be created because 'ports' is not specified
			INFO Kubernetes file "docker-compose\\templates\\rabbitmq-service.yaml" created
			INFO Kubernetes file "docker-compose\\templates\\consumer-deployment.yaml" created
			INFO Kubernetes file "docker-compose\\templates\\producer-deployment.yaml" created
			INFO Kubernetes file "docker-compose\\templates\\rabbitmq-deployment.yaml" created
			INFO chart created in "docker-compose\\"
		Result: C:\GitWS\k8training\rmqp-example\helm 
			Uploaded to: 
4. Created "Continuous Integration Pipeline" job, with dind:
	!!!!!!!!!!!!!upload to jobs github!!!!
	