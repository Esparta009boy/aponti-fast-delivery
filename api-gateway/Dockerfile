# ==========================================
# Estágio 1: Build (Compilação/Dependências)
# ==========================================
FROM node:18-alpine AS builder

WORKDIR /app

# Copia os arquivos de dependências
COPY package*.json ./

# Instala todas as dependências
RUN npm install

# Copia o código fonte
COPY . .

# ==========================================
# Estágio 2: Imagem Final (Otimizada e Leve)
# ==========================================
FROM node:18-alpine AS runner

WORKDIR /app

# Definindo variáveis de ambiente padrão flexíveis (sem credenciais hardcoded)
ENV NODE_ENV=production
ENV PORT=3000

# Copia apenas os artefatos necessários do estágio anterior
COPY --from=builder /app/package*.json ./
COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/ .

# Expõe a porta dinâmica
EXPOSE ${PORT}

# Executa como usuário não-root por segurança
USER node

CMD ["node", "server.js"]
