## API Gateway
un serveur qui agit comme un point d'entrée unique pour un ensemble d'APIs, jouant un rôle similaire à celui d'un reverse proxy pour les microservices
On a: 
- Order Service (port 3002)
- Payment Service (port 3001)
- API Gateway (port 3000)

Le docker file pour creer et exposer le port de l'API Gateway
![alt text](<Screenshot 2024-06-15 at 19.58.14.png>)
Expose le port 3000 et utilise les volumes pour stocker les modules Node.js ainsi que l'application.
![alt text](<Screenshot 2024-06-15 at 20.00.56.png>)

## Instanciation des Microservices dans l'API Gateway
![alt text](<Screenshot 2024-06-15 at 20.05.43.png>)

On injecte l'instance des microservices 
![alt text](<Screenshot 2024-06-15 at 20.03.24.png>)

On fait l'appel des microservices dans le service de l'API Gateway
![alt text](<Screenshot 2024-06-15 at 20.04.29.png>)


## Pour l'Order Service, voici les configurations :
Écoute sur le port 3001.
Instanciation du microservice et écoute sur le port 3001.
![alt text](<Screenshot 2024-06-15 at 20.08.05.png>)

Création de l'image du microsservicess dans le dockerfile: 
![alt text](<Screenshot 2024-06-15 at 20.09.06.png>)

Créaton du container order et mysql pour stocker les donnees 
![alt text](<Screenshot 2024-06-15 at 20.09.06-1.png>)

## Pour le Payment Service, voici les configurations :
Écoute sur le port 3002.
Création du conteneur MySQL pour stocker les données
![alt text](<Screenshot 2024-06-15 at 20.11.52.png>)



** Les différents services sont indépendants les uns des autres. Tous les microservices ne sont pas directement accessibles via leurs ports spécifiques, mais uniquement via l'API Gateway.

Pour l'API Gateway, le port 31000 est exposé et tous les appels sur ce port sont redirigés vers le port 3000
![alt text](<Screenshot 2024-06-15 at 20.17.08.png>)


## Configuration des Pods
Les différentes configurations des pods exécutant les microservices sont les suivantes : téléchargement des images api-gateway, order-service et payment-service, et définition des ports utilisés dans le Dockerfile.

![alt text](<Screenshot 2024-06-15 at 20.18.23.png>)

Voici le déploiement local sur Minikube. Cinq pods sont créés, dont trois pour les différents microservices. Les deux autres pods sont disponibles pour recréer un microservice en cas de panne.
![alt text](<Screenshot 2024-06-15 at 20.21.21.png>)