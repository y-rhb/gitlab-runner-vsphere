# Préparer un GitLab Runner sur vSphere

Un GitLab Runner exécute les tâches d’un pipeline. Dans le projet SLLYM, sa préparation était automatisée pour retrouver les mêmes outils et réglages d’une machine à l’autre.

## Dans ce dépôt

- [Préparation de l’hôte](ansible/roles/common/tasks/main.yml) — attend la fin de l’initialisation cloud-init, récupère les informations système et installe les paquets de base.

- [Docker](ansible/roles/docker/tasks/main.yml) — sépare l’installation du moteur de la configuration du service.
- [Outils d’infrastructure](ansible/roles/infra_tools/tasks/main.yml) — orchestre l’installation des clients utilisés par les pipelines.
- [Pare-feu](ansible/roles/firewalld/tasks/main.yml) et [SELinux](ansible/roles/selinux/tasks/main.yml) — appliquent des réglages propres au rôle de la machine.
- [Stockage](ansible/roles/disk_expansion/tasks/main.yml) — étend les volumes selon une disposition définie par l’inventaire.

## Projet d’origine et réutilisation

Le projet de fin d’études SLLYM, réalisé en équipe à l’ESGI, créait les machines sur vSphere avec Terraform, puis préparait et enregistrait les runners avec Ansible. Ce dépôt contient les six rôles de préparation de l’hôte. Le provisionnement Terraform et l’enregistrement auprès de GitLab demandent les éléments du déploiement complet.
