# Alternative Architecture Consideration

During the design phase, Kubernetes-based deployment using Amazon EKS was considered to provide orchestration capabilities such as automated scaling, rolling updates, and improved workload management.

For this implementation, an EC2-based deployment model was selected to prioritize:

* Faster deployment and validation cycles
* Lower infrastructure cost during assessment execution
* Simpler operational management for the application scale
* Reduced infrastructure overhead while maintaining production concepts

The architecture was designed in a way that supports future migration toward container orchestration platforms such as Kubernetes.

## Future Enhancements

Potential improvements for future iterations:

* Migrate workloads to Kubernetes (Amazon EKS)
* Implement Horizontal Pod Autoscaling
* Use Ingress Controllers for traffic routing
* Add container registry integration using Amazon ECR
* Introduce Infrastructure modules for Terraform reusability
* Implement centralized logging stack
* Deploy applications across multiple EC2 instances or node groups

## Architectural Trade-off

The EC2-based deployment approach provides lower operational complexity and cost efficiency while still demonstrating:

* Infrastructure as Code using Terraform
* Containerization using Docker
* Automated deployments through GitHub Actions
* Monitoring using CloudWatch
* Load balancing using Application Load Balancer
* Multi-container deployment architecture
