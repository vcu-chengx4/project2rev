Revature Project 2

Team Members:

Leader: Xianghe Cheng
Member 2: Ananda Magar
Member 3: Mohamed Bassiouni

Project 2 will be a group project. Groups will consist of 3 - 4 people. Each team must designate one member of the team to act as Team Leader. Then decide on a team name. Each team will choose a project from one of their member's Project 1's. Teams are allowed to create new namespaces on the SRE Cluster for Project 2. If done, the selected project must be deployed in the new namespace. Each team will follow an Agile approach. Daily Standups will happen separately for each group, led by the Team Leader.

Requirements:

    Each team must configure Prometheus to retrieve metrics from the deployed application
        Teams must create custom metrics through the micrometer API
            3 member teams must create at least 1 custom metric
            4 member teams must create at least 2 custom metrics
        These will be incorporated into the SLOs, so they should indicate something about the quality of the application
    Each team must define an SLO for their application.
        Must include error rates as well as latencies
        Must include their custom metrics
    Each team must define custom recording and alerting rules based on their SLOs
        These must follow the multi-window, multi-burn rate approach
    Each team must have a full DevOps pipeline built using Jenkins
        This pipeline must be configured through a Jenkinsfile and triggered in response to a webhook
        The project will be deployed with a canary deployment model
        Custom Dockerfiles must be designed and used
            No more usage of mvn spring-boot:build-image
            However, teams may design their Dockerfiles based on it
    Each team must create at least 1 Grafana dashboard to track all of the metrics associated with their SLO
        Teams with 4 members must also have additional panels
            Could be in a second dashboard
        Examples could be tracking relevant logs of the application or cpu/memory usage from Prometheus
        The more closely this additional dashboard indicates potential issue scenarios, the better
        The idea is to have visualizations that might indicate that a problem might occur soon, even if an alert has not fired yet

Technologies used: Java, OOP, Spring Boot, Docker, Grafana, Loki, Prometheus, Kubernetes

SLO objectives/goals:

Latency: Custom Metric - Execution time of GET users, POST register, and add-to-cart requests must be lower than 0.5s or 500ms.

Error rate: Http request errors and application error logs must not be over 90%.

Putting Application in Kubernetes:

Step 1: Install Postgres in Kubernetes by applying the files in this order:
  1. postgres-configmap.yml
  2. postgres-storage.yml
  3. postgres-statefulset.yml
  4. postgres-service.yml

Step 2: Kubectl edit postgres-service and make it LoadBalancer.

Step 3: Check postgres-service ClusterIP and copy and paste that into the application.properties of project 1 and upload the changes to dockerhub.

Step 4: Apply the project2.yml in Kubernetes and also make project2-service LoadBalancer.

Step 5: Install Prometheus and Grafana via Helm.

Step 6: Edit Prometheus-server, prometheus-alertmanager, and Grafana services into LoadBalancer.

Step 7: Use kubectl edit configmap prometheus-server and add custom targets in the "prometheus.yml: |" section.
*To connect your custom metrics in your project, make sure the targets in the static_configs: is [minikube-ip]:[Port].

Step 8: Add custom rules in the alert-rules | section of the configmap

Step 9: Portforward prometheus or grafana to the desired ports if you need to view them externally.  

Step 10: Import Project 2-1655438298965 into Grafana.

