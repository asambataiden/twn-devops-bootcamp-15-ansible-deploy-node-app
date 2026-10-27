# Capstone 02 — Ansible Kubernetes Deployment Component

This branch is the Ansible half of **TechWorld with Nana Capstone 02 — Automate Kubernetes Deployment**.

**Main Capstone 02 submission overview (Terraform branch):**  
https://github.com/asambataiden/twn-devops-bootcamp-12-terraform-terraform-learn/tree/feature/project-14-ansible-eks-k8s-deploy-to-eks-with-terraform

## What this code does

The `deploy-to-k8s.yaml` playbook runs locally, reads `k8s-vars.yaml`, creates the Kubernetes namespace `my-app`, and applies `nginx-config.yaml`. That manifest declares one Nginx Pod replica via a Deployment and exposes port 80 through a LoadBalancer Service. The variables reference the intended EKS cluster `myapp-eks-cluster` in region `eu-north-1`.

## Files

- [deploy-to-k8s.yaml](deploy-to-k8s.yaml) — Kubernetes namespace and application tasks
- [k8s-vars.yaml](k8s-vars.yaml) — target names, region, kubeconfig path
- [nginx-config.yaml](nginx-config.yaml) — Deployment and Service
- [ansible.cfg](ansible.cfg) — historical Ansible configuration

## Status and safe verification

The source code was reviewed, but successful playbook execution, Pod readiness and HTTP availability **have not been independently verified** as part of this submission review. Use an authorized environment and verify the intended AWS identity, cluster context and namespace before any resource-changing run.

The playbook currently uses the historical Kubernetes `k8s` module name. For maintainability, document/install a compatible `kubernetes.core` collection and use `kubernetes.core.k8s` explicitly in a reviewed revision. The Nginx image is currently `nginx:latest`, which should be pinned before reproducible releases. The current `ansible.cfg` disables SSH host-key verification globally, which is not recommended. The K8s localhost tasks do not themselves require bypassing SSH host-key checking.

## What I learned

I learned how Ansible can call the Kubernetes API to create a namespace and deploy application manifests, using externalized environment variables and kubeconfig. I also learned to verify cluster targets, dependency versions, runtime deployment health, and the difference between having a working playbook in Git and proving it executed successfully.

## Acceptance checklist

- [x] Namespace and workload deployment code present
- [x] Linked to Terraform infrastructure source
- [ ] Compatible dependency installation and syntax check evidence
- [ ] Verified playbook execution against intended EKS cluster
- [ ] Pod readiness and HTTP response evidence
- [ ] Cost, security and cleanup review

**Do not create or destroy EKS infrastructure just to complete documentation.**
