# Network Attack Analysis – SYN Flood Investigation  
**Projet issu du Google Cybersecurity Professional Certificate**

## Objectif du projet
L’objectif de ce module était d’analyser une interruption de service affectant un site web et de déterminer si l’incident résultait d’une attaque réseau.  
L’investigation a permis d’identifier un **SYN Flood (DoS)** responsable de la saturation du serveur.

---

## Résumé exécutif
Le serveur web cesse de répondre après avoir reçu un volume important de requêtes SYN.  
La nature répétitive et non finalisée du handshake TCP révèle un **flooding SYN**, saturant la table de connexions et bloquant les utilisateurs légitimes.

Cette analyse démontre un raisonnement SOC structuré et aligné avec les bonnes pratiques enseignées dans le certificat Google.

---

## Contexte & symptômes observés
- Message observé : **connection timeout**
- Nombre élevé de requêtes TCP SYN dans les logs
- Absence d’ACK de finalisation du handshake
- Saturation des ressources du serveur

Ces éléments indiquent une attaque visant à **empêcher la création de connexions légitimes**.

---

## Analyse technique

### 1. Handshake TCP normal
1. SYN → demande de connexion  
2. SYN-ACK → confirmation du serveur  
3. ACK → finalisation de la connexion  

### 2. Dysfonctionnement observé
Le serveur reçoit des **SYN** mais ne reçoit jamais le **ACK final**, ce qui crée des connexions demi-ouvertes.  
Celles-ci épuisent les ressources de la table de sessions, rendant le service indisponible.


---

## Cause de l'incident : SYN Flooding
L’analyse met en évidence une attaque de type :

### **SYN Flood (Denial of Service)**  
Objectifs probables :
- Saturer la mémoire
- Interrompre le service web
- Détériorer l’expérience utilisateur ou masquer une action secondaire

---

## Compétences développées  
*(acquises dans le cadre du Google Cybersecurity Professional Certificate)*

- Analyse de trafic réseau et compréhension du handshake TCP
- Détection d’un DoS par comportement réseau
- Investigation technique basée sur des logs et paquets
- Rédaction d’un rapport d’incident professionnel
- Réflexion structurée adoptée par les analystes SOC

---

## Recommandations

### Techniques
- Activer les **SYN Cookies**
- Configurer un firewall/IPS pour limiter les SYN par seconde
- Mettre en place du **rate limiting**
- Utiliser un WAF ou une protection DDoS cloud

### Détection
- Alertes sur taux anormal de connexions demi-ouvertes
- Surveillance du backlog TCP
- Corrélation temps réel via SIEM

---

## Conclusion
L’analyse confirme qu’un **SYN Flooding** est à l’origine de l’indisponibilité du service.  
Ce projet reflète la capacité à appliquer les concepts fondamentaux enseignés dans le **Google Cybersecurity Professional Certificate**, en adoptant une approche méthodique orientée analyse, détection et mitigation.

---

