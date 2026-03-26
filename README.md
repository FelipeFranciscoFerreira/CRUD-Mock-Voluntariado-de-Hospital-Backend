# Hospital Voluntário - Backend API

[cite_start]Esta é uma API REST desenvolvida para o gerenciamento de um sistema de voluntariado em um hospital fictício[cite: 1]. [cite_start]A plataforma centraliza o controle de usuários, vagas de trabalho voluntário e candidaturas, integrando um sistema de gamificação baseado em pontos de recompensa[cite: 1].

## Tecnologias Utilizadas

* [cite_start]**Ambiente de Execução:** Node.js[cite: 1].
* [cite_start]**Linguagem:** TypeScript para desenvolvimento tipado e seguro[cite: 1].
* [cite_start]**Framework Web:** Express 5[cite: 1].
* [cite_start]**ORM:** Prisma para modelagem e consulta ao banco de dados PostgreSQL[cite: 1].
* [cite_start]**Segurança:** Autenticação via JSON Web Token (JWT) e criptografia de senhas com Bcrypt[cite: 1].
* [cite_start]**Validação de Dados:** Zod para validação de esquemas e tipos[cite: 1].

## Funcionalidades Principais

### Autenticação e Gestão de Usuários
* [cite_start]**Controle de Acesso:** Implementação de perfis de usuário comum e administrador através de middlewares de autenticação[cite: 1].
* [cite_start]**Cadastro Completo:** Coleta de dados como CPF, escolaridade, profissão e endereço[cite: 1].
* [cite_start]**Sessão Segura:** Autenticação baseada em tokens JWT com tempo de expiração definido[cite: 1].

### Gestão de Vagas
* [cite_start]**Administração:** Criação, atualização e exclusão de vagas por usuários administradores[cite: 1].
* [cite_start]**Categorização:** Classificação de vagas por tipo (ex: Idosos, Crianças) e definição de pontos de recompensa[cite: 1].
* [cite_start]**Listagem Dinâmica:** Filtros por tipo de vaga, pontuação mínima e status (Aberta/Fechada)[cite: 1].

### Fluxo de Candidatura e Gamificação
* [cite_start]**Inscrição:** Processo de candidatura vinculado ao ID do usuário autenticado[cite: 1].
* [cite_start]**Processamento Automático:** Ao aprovar uma candidatura, o sistema encerra a vaga, rejeita demais candidatos pendentes e credita os pontos ao voluntário selecionado[cite: 1].
* [cite_start]**Ranking:** Sistema de Leaderboard que ordena usuários pelo total de pontos acumulados em tarefas concluídas[cite: 1].

## Estrutura de Dados (Prisma)

[cite_start]O esquema do banco de dados é composto por três entidades principais[cite: 1]:

* [cite_start]**Usuario:** Armazena informações pessoais, credenciais, status de administrador e pontuação total[cite: 1].
* [cite_start]**Vagas:** Define o título, descrição, tipo, data da tarefa e pontos de recompensa[cite: 1].
* [cite_start]**UsuarioVagas:** Gerencia o relacionamento entre voluntários e vagas, controlando o status da aplicação (Pendente, Aprovado, Rejeitado, Concluido)[cite: 1].

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
| POST | /auth/signup | [cite_start]Cadastro de novos usuários[cite: 1]. |
| POST | /vagas | [cite_start]Criação de novas oportunidades (Admin)[cite: 1]. |
| GET | /leaderboard | [cite_start]Consulta ao ranking de pontuação[cite: 1]. |
| PATCH | /candidatura/aprovar/:id | [cite_start]Aprovação de voluntário e distribuição de pontos[cite: 1]. |
