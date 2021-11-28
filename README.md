# k8project
Advanced Devops project by Ohad Kless, HP Indigo

Did the following:
1. Installed Jenkins:
	helm repo add jenkinsrepo https://charts.jenkins.io
	helm install jenkins jenkinsrepo/jenkins --set controller.serviceType=NodePort
	minikube service jenkins
	Added secret text (created in Github GGGH_SECRET, okless123, and put in Jenkins sesttings)
2. Created "Continuous Integration Pipeline" job, with dind:
	Does the following:
		a. Creates 2 Docker images: docker-producer and docker-consumer
		b. Clones my repo
		c. Builds images
		d. Push images to DockerHub:
			Created repo k8project https://hub.docker.com/repository/docker/okless/k8project
			Created access token in https://hub.docker.com/settings/security (see https://www.youtube.com/watch?v=alQQ84M4CYU)
			can now do in Jenkins: docker login -u okless
			Add this to my Jenkins credentials (user name okless and password c50a32a8-e47a-4534-a955-bedd7ba8bfd7, id okless-dockerhub)
			See Jenkins Continuous Integration Pipeline here: https://github.com/okless71/k8project/blob/main/jenkins-pipelines/Continuous%20Integration%20Pipeline.yaml
			Images are here: 
				https://hub.docker.com/repository/docker/okless/docker-consumer
				https://hub.docker.com/repository/docker/okless/docker-producer
	Questions:
		- How to avoid having password in pipeline?
3. Converted docker-compose yaml to Helm chart with tool kompose:
	Cloned https://github.com/avielb/rmqp-example
	Install kompose and convert compser files to helm chart:
		curl -L https://github.com/kubernetes/kompose/releases/download/v1.24.0/kompose-windows-amd64.exe -o kompose.exe
	chmod +x kompose
	Copy compose file to location of kompose
	cd /c/GitWS/k8training/rmqp-example
	/c/temp/kompose.exe convert -c
	helm create deployk8
	Override with kompose result
	Upload helm chart to Githubas new repo: https://github.com/okless71/helm-charts
4. Upload to helm hub: https://artifacthub.io/: 
	Followed this tutorial to prepare for upload chart: https://tech.paulcz.net/blog/creating-a-helm-chart-monorepo-part-1/
	Download cr from https://github.com/helm/chart-releaser/releases
	
	
