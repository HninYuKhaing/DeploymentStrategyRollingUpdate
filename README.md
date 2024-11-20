Deployment Strategy: Rolling Update
---
This repository demonstrates how to perform a Rolling Update Deployment using Kubernetes. The project includes a step-by-step guide, configuration files, and practical examples to help you understand and implement rolling updates effectively.

---
Repository Structure
---

Namespace Configuration:
---
Defines a team4 namespace to isolate the deployment.

Deployment Configurations:
---
Three separate deployment configurations for team4-app, each illustrating an update to the application's features:
1. Features available: USD, SGD
2. Features available: USD, SGD, JPY
3. Features available: USD, SGD, JPY, EUR
Uses the RollingUpdate strategy to demonstrate how gradually replaces old pods with new ones in a Kubernetes deployment, ensuring minimal downtime and continuous availability of your application.

Service Configuration:
---
Exposes the team4-app deployment as a service (team4-app-svc) on port 80.

Utility Pod:
---
Includes a dnstools pod for testing DNS resolution within the namespace.

Deployment Steps
---
1. Clone the Repository:
</BR>git clone https://github.com/HninYuKhaing/DeploymentStrategyRollingUpdate.git
</BR>cd DeploymentStrategyRollingUpdate
2. Deploy the Application:
</BR>kubectl apply -f deployment1.yaml 
3. Create the Service:
</BR>kubectl apply -f service.yaml 
4. Launch Utility Pod:
</BR>kubectl apply -f dnstools.yaml

Access the Application
---
Get the Deployment, Service details:
</BR>Open new terminal
</BR>watch kubectl get all -n team4 -o wide

Testing DNS with dnstools
---
</BR><B>Open new terminal</B>
</BR>kubectl exec -it pod/dnstools -n team4 -- sh
</BR>while true; do curl http://team4-app-svc; sleep 0.5; done

</BR><B>Open new terminal</B>
</BR>watch kubectl rollout history  deployment/team4-app -n team4

</BR><B>Open new terminal</B>
</BR>watch kubectl rollout status  deployment/team4-app -n team4

</BR><B>Open new terminal</B>
</BR>Deploy the New Application:
</BR>kubectl apply -f deployment2.yaml
</BR>Look for the changes in other terminals

</BR><B>Open new terminal</B>
</BR>Deploy the New Application:
</BR>kubectl apply -f deployment3.yaml
</BR>Look for the changes in other terminals

</BR><B>Undo changes to previous</B>
</BR>kubectl rollout undo deployment/team4-app -n team4

</BR><B>Undo changes to revision-1</B>
</BR>kubectl rollout undo deployment/team4-app -n team4 --to-revision=1

Cleanup
---
kubectl delete namespace team4

Key Features of RollingUpdate Strategy
---
- Replace pods incrementally to avoid service disruptions.
- Built-in rollback capability for easy recovery.
- Monitor deployment status in real-time.

YouTube Demo:
---
https://youtu.be/zJsvJHk-Ou4?si=L3SNeBm0rNbQVOGk




