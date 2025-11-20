Ce document décrit un diagramme (disponible en SVG et PNG) qui illustre une proposition de solution pour gérer les certificats TLS internes dans un environnement Kubernetes privé.

**Objectif principal :** Présenter une solution pour garantir que les services internes disposent de certificats TLS reconnus et valides, éliminant ainsi les problèmes liés à l'absence de confiance ou à la nécessité de configurations complexes pour les services consommateurs.

**Points clés :**

*   **Flux du certificat :** Le diagramme montre comment Let's Encrypt pourrait valider la propriété du domaine via un défi DNS-01 auprès du fournisseur DNS public, permettant ainsi d'obtenir un certificat valide pour le cluster Kubernetes via `cert-manager` et l'Ingress/Gateway.
*   **Architecture:** Le diagramme délimite clairement les dépendances publiques (Let's Encrypt, fournisseur DNS) et privées (cluster Kubernetes, utilisateurs internes).
*   **Avantages:** Le diagramme clarifie l'architecture TLS proposée et sert de référence visuelle pour comprendre la solution envisagée, garantissant une infrastructure de confiance pour les services internes.
*   **Formats disponibles:** Le diagramme est disponible en SVG (pour une utilisation programmatique et une qualité supérieure) et en PNG (pour un partage rapide).

En résumé, le diagramme explique comment un cluster Kubernetes privé *pourrait* obtenir des certificats TLS publiquement fiables (via Let's Encrypt et DNS-01) pour ses services internes, offrant une solution stable et fiable pour les applications et services, sans nécessiter de configurations spéciales ou de contournements liés à la confiance des certificats.
