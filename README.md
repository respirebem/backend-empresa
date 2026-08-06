# Respire Bem - Backend Empresa

API REST em Spring Boot para o projeto **Respire Bem**, plataforma de gestão de bem-estar dos colaboradores.

## Visão geral
O backend gerencia empresas, usuários, colaboradores, profissionais, departamentos, especialidades, check-ins e dashboards de saúde mental.
A aplicação oferece autenticação JWT, perfis de acesso e dados estruturados para integração com o front-end.

## Principais funcionalidades
- Cadastro inicial de empresa e usuário ADMIN
- Autenticação segura com JWT
- Gerenciamento de usuários e permissões
- Cadastro e listagem de colaboradores
- Cadastro e listagem de profissionais e especialidades
- Consulta de departamentos
- Registro de check-ins de colaboradores
- Histórico de check-ins por usuário autenticado
- Dashboard com métricas agregadas para visualização

## Tecnologias
- Java 17
- Spring Boot 3.5
- Spring Security
- JWT (JSON Web Tokens)
- Spring Data JPA
- PostgreSQL
- SpringDoc OpenAPI (Swagger)

## Endpoints principais
### Autenticação
- `POST /auth/registrar/empresa` - registra empresa e usuário ADMIN
- `POST /auth/login` - autentica e retorna token JWT

> Para endpoints protegidos, use o header: `Authorization: Bearer <token>`

### Empresa
- `GET /empresa/meus-dados` - dados da empresa do usuário autenticado
- `PUT /empresa/atualizar-dados?nomeEmpresa={nome}&cnpjEmpresa={cnpj}` - atualiza nome e CNPJ

### Usuário (role ADMIN)
- `GET /usuario/listarUsuarios` - lista todos usuários
- `PUT /usuario/alterar-credenciais/{idUsuario}?novoEmail={email}&novaSenha={senha}` - altera credenciais
- `DELETE /usuario/deletar/{idUsuario}` - remove usuário

### Departamento
- `GET /departamento/listarDepartamentos` - lista departamentos

### Especialidade
- `GET /especialidade/listarEspecialidades` - lista especialidades

### Colaborador
- `POST /colaborador/cadastrarColaborador` - cadastra colaborador vinculado à empresa autenticada
- `GET /colaborador/listarColaboradores` - lista colaboradores
- `GET /colaborador/buscarNomeColaborador?nomeColaborador={nome}` - busca colaborador por nome
- `PUT /colaborador/editarColaborador/{idColaboradorAlterar}` - atualiza colaborador
- `DELETE /colaborador/deletar/{idColaborador}` - remove colaborador

### Profissional
- `POST /profissional/cadastrarProfissional` - cadastra profissional vinculado à empresa autenticada
- `GET /profissional/listarProfissionais` - lista profissionais
- `GET /profissional/buscarNomeProfissional?nomeProfissional={nome}` - busca profissional por nome
- `PUT /profissional/editarProfissional/{idProfissionalAlterar}` - atualiza profissional
- `DELETE /profissional/deletar/{idProfissional}` - remove profissional

### Check-in
- `POST /checkin/fazerCheckIn` - registra check-in de colaborador
- `GET /checkin/historico` - retorna histórico de check-ins do usuário autenticado

### Dashboard
- `GET /dashboard/dados` - retorna dados agregados para gráficos ou visão geral

## Configuração local
### Pré-requisitos
- Java 17
- PostgreSQL
- Git

### Banco de dados padrão
O backend usa o `application.properties` em `empresa/src/main/resources` com as seguintes configurações:
- URL: `jdbc:postgresql://localhost:5432/empresa`
- Usuário: `postgres`
- Senha: `123`

> Ajuste os valores se necessário no arquivo `empresa/src/main/resources/application.properties`.

### Passo a passo para rodar o backend
1. Abra o terminal e vá para a pasta do projeto:
   - `cd /caminho/para/backend-empresa/empresa`
2. Crie o banco de dados PostgreSQL `empresa`:
   - `createdb -U postgres empresa`
   - ou use uma interface gráfica como pgAdmin
3. Execute a aplicação:
   - `./mvnw spring-boot:run`
   - no Windows PowerShell: `./mvnw.cmd spring-boot:run`
4. Acesse a API em:
   - `http://localhost:8080` (porta padrão do backend)
5. Documentação Swagger:
   - `http://localhost:8080/swagger-ui.html`

> Observação: o Apache/XAMPP do front-end pode rodar em outra porta, sem conflito com o backend em `8080`.

### Executar testes
- `./mvnw test`
- no Windows PowerShell: `./mvnw.cmd test`

## Integração com o front-end
O front-end do projeto está em:
- `https://github.com/respirebem/frontend-empresa.git`

### Como integrar
1. Clone o repositório front-end:
   - `git clone https://github.com/respirebem/frontend-empresa.git`
2. Ajuste a URL do backend no front-end:
   - Se o backend estiver local: `http://localhost:8080`
   - Se o backend for exposto por ngrok: use a URL pública `https://xxxxxx.ngrok.io`
3. No front-end, garanta que as requisições protegidas enviem o header:
   - `Authorization: Bearer <token>`
4. Use o cadastro inicial em `/auth/registrar/empresa` para criar o primeiro usuário ADMIN.
5. Faça login em `/auth/login` e utilize o token retornado para acessar as demais rotas.

### Integração via Apache/XAMPP
- Se o front-end estiver hospedado em Apache/XAMPP em outra porta, ajuste a URL do frontend para usar essa porta.
- Exemplo de acesso: `http://localhost:<porta>/frontend-empresa`
- Garanta que a URL de backend no front-end aponte para a mesma origem do backend ou para a URL do ngrok.

### Observações para integração
- O front-end deve consumir as rotas de colaboradores, profissionais, especialidades, departamentos, check-ins e dashboard.
- Se houver bloqueio de CORS, configure o backend para liberar a origem do front-end ou execute o front-end e o backend na mesma origem.
- Se usar ngrok, a URL pública do ngrok deve ser usada no front-end e o backend precisa estar ativo localmente.

## Status do projeto
- Backend finalizado e funcional
- Segurança com JWT e senhas criptografadas via BCrypt
- Relacionamentos entre empresa, colaboradores, profissionais e departamentos implementados

## Contato
Este repositório contém o backend da solução Respire Bem. Para dúvidas sobre a API, consulte os controladores em `empresa/src/main/java/com/empresa/empresa/Controllers`.


