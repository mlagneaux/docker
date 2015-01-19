docker
======

Different Dockerfile to build Docker images :
- Alfresco prerequisites : a container with the prerequisites of the latest version of Alfresco
- Alfresco : a container with the latest version of Alfresco (currently 5.0c)
	=> TODO Install and configure SolR instead of Lucene
- ElasticSearch 1.4.2 image
- NodeJS image
- Tomcat 7 image

All images are pushed to Docker hub : https://registry.hub.docker.com/repos/mlagneaux/
