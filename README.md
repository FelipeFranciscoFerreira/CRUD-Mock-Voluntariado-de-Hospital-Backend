# Hospital Voluntário - Backend API

Esta é uma API REST desenvolvida para o gerenciamento de um sistema de voluntariado em um hospital fictício[cite: 1]. A plataforma centraliza o controle de usuários, vagas de trabalho voluntário e candidaturas, integrando um sistema de gamificação baseado em pontos de recompensa[cite: 1].

## Tecnologias Utilizadas

* **Ambiente de Execução:** Node.js[cite: 1].
* **Linguagem:** TypeScript para desenvolvimento tipado e seguro[cite: 1].
* **Framework Web:** Express 5[cite: 1].
* **ORM:** Prisma para modelagem e consulta ao banco de dados PostgreSQL[cite: 1].
* **Segurança:** Autenticação via JSON Web Token (JWT) e criptografia de senhas com Bcrypt[cite: 1].
* **Validação de Dados:** Zod para validação de esquemas e tipos[cite: 1].

## Funcionalidades Principais

### Autenticação e Gestão de Usuários
* **Controle de Acesso:** Implementação de perfis de usuário comum e administrador através de middlewares de autenticação[cite: 1].
* **Cadastro Completo:** Coleta de dados como CPF, escolaridade, profissão e endereço[cite: 1].
* **Sessão Segura:** Autenticação baseada em tokens JWT com tempo de expiração definido[cite: 1].

### Gestão de Vagas
* **Administração:** Criação, atualização e exclusão de vagas por usuários administradores[cite: 1].
* **Categorização:** Classificação de vagas por tipo (ex: Idosos, Crianças) e definição de pontos de recompensa[cite: 1].
* **Listagem Dinâmica:** Filtros por tipo de vaga, pontuação mínima e status (Aberta/Fechada)[cite: 1].

### Fluxo de Candidatura e Gamificação
* **Inscrição:** Processo de candidatura vinculado ao ID do usuário autenticado[cite: 1].
* **Processamento Automático:** Ao aprovar uma candidatura, o sistema encerra a vaga, rejeita demais candidatos pendentes e credita os pontos ao voluntário selecionado[cite: 1].
* **Ranking:** Sistema de Leaderboard que ordena usuários pelo total de pontos acumulados em tarefas concluídas[cite: 1].

## Estrutura de Dados (Prisma)

O esquema do banco de dados é composto por três entidades principais[cite: 1]:

* **Usuario:** Armazena informações pessoais, credenciais, status de administrador e pontuação total[cite: 1].
* **Vagas:** Define o título, descrição, tipo, data da tarefa e pontos de recompensa[cite: 1].
* **UsuarioVagas:** Gerencia o relacionamento entre voluntários e vagas, controlando o status da aplicação (Pendente, Aprovado, Rejeitado, Concluido)[cite: 1].

## Configuração do Ambiente

### Instalação
1. Instale as dependências do projeto:
   ```bash
   npm install
   ```

2. Configure as variáveis de ambiente em um arquivo `.env`:
   ```env
   DATABASE_URL="postgresql://usuario:senha@localhost:5432/hospital_db"
   JWT_SECRET="sua_chave_secreta"
   ```

3. Sincronize o banco de dados:
   ```bash
   npx prisma migrate dev
   ```

### Execução
* Para iniciar em ambiente de desenvolvimento:
  ```bash
  npm run dev
  ```
* Para gerar o build e iniciar em produção:
  ```bash
  npm run build
  npm start
  ```

## Principais Endpoints

| Método | Rota | Descrição |
| :--- | :--- | :--- |
| POST | /auth/signup | Cadastro de novos usuários[cite: 1]. |
| POST | /vagas | Criação de novas oportunidades (Admin)[cite: 1]. |
| GET | /leaderboard | Consulta ao ranking de pontuação[cite: 1]. |
| PATCH | /candidatura/aprovar/:id | Aprovação de voluntário e distribuição de pontos[cite: 1]. |
