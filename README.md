# 🚀 Aponti Fast Delivery - Infraestrutura Ágil e Alta Disponibilidade

Este repositório contém a reestruturação completa da arquitetura de microsserviços da startup **Aponti Fast Delivery**, utilizando práticas modernas de DevOps, otimização de imagens Docker e orquestração de alta disponibilidade via Docker Swarm.

---

## 🏗️ Arquitetura do Sistema

O sistema é composto por 4 microsserviços e 1 banco de dados:
* **API Gateway**: Porta de entrada pública (Porta 80 -> 3000).
* **Product Service**: Gestão de produtos (3 réplicas).
* **Inventory Service**: Gestão de estoque (3 réplicas).
* **Order Service**: Gestão de pedidos (3 réplicas).
* **MongoDB**: Banco de dados (1 réplica isolada no nó Manager com volume persistente).

---

## 🛠️ Tecnologias e Melhores Práticas Aplicadas

1. **Multi-Stage Build**: Redução do tamanho final das imagens para menos de 200MB utilizando Alpine Linux.
2. **Segurança & Isolamento**: Nenhuma porta interna exposta publicamente. Variáveis de ambiente configuradas via `ENV`.
3. **Rede Overlay Criptografada**: Comunicação segura entre os serviços no cluster Swarm através da rede `aponti-net`.
4. **Limites de Recursos**: Restrições de CPU e memória aplicadas para evitar exaustão do servidor.

---

## 🚀 Como Executar o Cluster Docker Swarm

### 1. Inicializar o Cluster no Nó Manager
```bash
docker swarm init

2. Criar a Rede Overlay Segura
Bash
docker network create --driver overlay --opt encrypted aponti-net

3. Fazer o Deploy da Stack de Produção
Bash
docker stack deploy -c docker-compose.yml aponti

4. Verificar o Status dos Serviços e Réplicas
Bash
docker stack services aponti

5. Verificar a Alocação dos Contêineres nos Nós
Bash
docker service ls
