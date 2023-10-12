
# Pedelogo Catalogo

Projeto para testar disponibilidade SelfHealing no Kubernetes



## Features

- Cadastro de Produtos
- Gerenciamento de disponibilidade

## Installation

Instalando meu projeto, utilizando k3d

```bash
# Criando cluster
k3d cluster create  -p "8080:30000@loadbalancer"

# Instalando projeto
kubectl apply -f ./ -R

# Link de acesso
http://127.0.0.1:8080/swagger
```

## Documentation



        # Disponibilidade - POD
        readinessProbe:
          httpGet:
            path: /read
            port: 80
            scheme: HTTP
          periodSeconds: 5 
          timeoutSeconds: 1 
          failureThreshold: 3 
        
        # Inicializaçao  - POD
        startupProbe:
          httpGet:
            path: /health
            port: 80
            scheme: HTTP
          failureThreshold: 10
          periodSeconds: 30

        # Saude - POD
        livenessProbe:
          httpGet:
            path: /health
            port: 80
            scheme: HTTP
          initialDelaySeconds: 5
          periodSeconds: 5 
          timeoutSeconds: 3 
          failureThreshold: 