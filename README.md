# Easybulk-K8s-BIAT

Dépôt contenant les fichiers de configuration Kubernetes pour déployer la plateforme EasyBulk de messagerie et d’analyse, **conçu pour être adapté** et utilisé en production chez BIAT.

---
## Les composants principaux de l'application Easybulk v3.0

| Composant           | Description                                                             |
| ------------------- | ----------------------------------------------------------------------- |
| **Frontend**        | Interface utilisateur Angular pour la plateforme EasyBulk               |
| **Backend**         | API Spring Boot gérant la logique métier et l’accès aux données         |
| **MySQL**           | Base de données relationnelle pour stocker les informations principales |
| **MongoDB**         | Base NoSQL pour stocker certaines données analytiques                   |
| **Redis**           | Cache mémoire pour améliorer les performances                           |
| **Centrifugo**      | Service de websocket pour les notifications en temps réel               |
| **Airflow**         | Orchestrateur de tâches pour les DAGs et automatisation                 |
| **Superset**        | Dashboard et analytics pour les données                                 |
| **Keycloak**        | Authentification et gestion des utilisateurs                            |
| **Kannel**          | Gateway SMS pour l’envoi et la réception                                |
| **SMPP Simulator**  | Simulateur pour tests de messagerie SMPP                                |
| **Caddy / Traefik** | Reverse proxy et Ingress pour le routage HTTP/HTTPS (A remplacer)       |

---
## Services et points d’accès

| Service | Route | Path | Port |
|---------|-------|------|------|
| superset | analytics.easybulk.intra |  | 80 |
| webserver | airflow.easybulk.intra |  | 7071 |
| back-ct-service | backct.easybulk.intra | /services | 9002 |
| keycloak-auth | app.easybulk.intra | /auth | 80 |
| esb-back | app.easybulk.intra | /api | 9000 |
| front | app.easybulk.intra |  | 80 |
---
## Adaptations prévues pour s'adapter à OpenShift

- **Ingress → Routes OpenShift** : Les services exposés via Ingress seront adaptés pour être exposés avec des **Routes** OpenShift.  
- **Dynamic Provisioning via NFS → ODF** : Les volumes persistants seront provisionnés dynamiquement sur **OpenShift Data Foundation (ODF)**.  
- **Storage Racks** : Les volumes seront attachés aux racks de stockage ODF pour garantir la haute disponibilité et la tolérance aux pannes.
