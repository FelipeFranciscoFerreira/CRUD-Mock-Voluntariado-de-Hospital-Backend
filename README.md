# Hospital Voluntário - Backend API

Esta é uma API REST desenvolvida para o gerenciamento de um sistema de voluntariado em um hospital fictício. A plataforma centraliza o controle de usuários, vagas de trabalho voluntário e candidaturas, integrando um sistema de gamificação baseado em pontos de recompensa.

## Tecnologias Utilizadas

* **Ambiente de Execução:** Node.js.
* **Linguagem:** TypeScript para desenvolvimento tipado e seguro.
* **Framework Web:** Express 5.
* **ORM:** Prisma para modelagem e consulta ao banco de dados PostgreSQL.
* **Segurança:** Autenticação via JSON Web Token (JWT) e criptografia de senhas com Bcrypt.
* **Validação de Dados:** Zod para validação de esquemas e tipos.

## Funcionalidades Principais

### Autenticação e Gestão de Usuários
* **Controle de Acesso:** Implementação de perfis de usuário comum e administrador através de middlewares de autenticação.
* **Cadastro Completo:** Coleta de dados como CPF, escolaridade, profissão e endereço.
* **Sessão Segura:** Autenticação baseada em tokens JWT com tempo de expiração definido.

### Gestão de Vagas
* **Administração:** Criação, atualização e exclusão de vagas por usuários administradores.
* **Categorização:** Classificação de vagas por tipo (ex: Idosos, Crianças) e definição de pontos de recompensa.
* **Listagem Dinâmica:** Filtros por tipo de vaga, pontuação mínima e status (Aberta/Fechada).

### Fluxo de Candidatura e Gamificação
* **Inscrição:** Processo de candidatura vinculado ao ID do usuário autenticado.
* **Processamento Automático:** Ao aprovar uma candidatura, o sistema encerra a vaga, rejeita demais candidatos pendentes e credita os pontos ao voluntário selecionado.
* **Ranking:** Sistema de Leaderboard que ordena usuários pelo total de pontos acumulados em tarefas concluídas.

## Estrutura de Dados (Prisma)

O esquema do banco de dados é composto por três entidades principais:

* **Usuario:** Armazena informações pessoais, credenciais, status de administrador e pontuação total.
* **Vagas:** Define o título, descrição, tipo, data da tarefa e pontos de recompensa.
* **UsuarioVagas:** Gerencia o relacionamento entre voluntários e vagas, controlando o status da aplicação (Pendente, Aprovado, Rejeitado, Concluido).

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
| POST | /auth/signup | Cadastro de novos usuários. |
| POST | /vagas | Criação de novas oportunidades (Admin). |
| GET | /leaderboard | Consulta ao ranking de pontuação. |
| PATCH | /candidatura/aprovar/:id | Aprovação de voluntário e distribuição de pontos. |
