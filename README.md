# Documentação Técnica do Projeto Aluno Online

## 1. **Descrição Geral**
O **Aluno Online** é um sistema backend desenvolvido em **Java** usando o framework **Spring Boot**. Ele gerencia informações relacionadas a alunos, disciplinas, professores e matrículas em um ambiente acadêmico. A documentação fornece detalhes técnicos do código, arquitetura e funcionalidades.

- **Linguagem**: Java (versão 17)
- **Framework**: Spring Boot
- **Banco de Dados**: PostgreSQL
- **Gerenciador de Dependências**: Maven
- **Documentação de API**: Swagger (via SpringDoc)

---

## 2. **Arquitetura do Projeto**
### Estrutura de Pastas
- **`src/main/java/br/com/alunoonline/api/`**
  - **`controller/`**: Controladores que gerenciam os endpoints da API.
  - **`service/`**: Contém a lógica de negócios.
  - **`model/`**: Define as entidades que representam as tabelas do banco de dados.
  - **`repository/`**: Interfaces responsáveis pela comunicação com o banco de dados.
  - **`config/`**: Configurações adicionais da aplicação, como o Swagger.
- **`src/main/resources/`**
  - Arquivo `application.properties`: Configurações como URL do banco, credenciais e outras variáveis de ambiente.

### Principais Componentes
1. **Controller**: Define os endpoints e gerencia as requisições HTTP.
   - **Propósito**: Expõe as funcionalidades do sistema para interações externas, como criação, leitura, atualização e exclusão de recursos.
   - **Exemplo**: `AlunoController.java` gerencia operações CRUD para a entidade `Aluno`.
   
2. **Service**: Contém a lógica de negócios da aplicação.
   - **Propósito**: Implementa regras de negócio e interage com repositórios.
   - **Exemplo**: `AlunoService.java` é responsável por validar dados e processar as operações de CRUD.

3. **Model**: Representa as entidades do banco de dados.
   - **Propósito**: Mapeia os dados de objetos Java para tabelas do banco de dados, com a ajuda do JPA (Java Persistence API).
   - **Exemplo**: `Aluno.java` contém atributos como `id`, `nome`, `cpf`, e `email`.

4. **Repository**: Define as interfaces de persistência de dados.
   - **Propósito**: Facilita a comunicação com o banco de dados, proporcionando métodos para salvar, atualizar, deletar e buscar entidades.
   - **Exemplo**: `AlunoRepository.java` é uma interface que estende `JpaRepository`, fornecendo funcionalidades para gerenciar os alunos no banco.

---

## 3. **Funcionalidades**
### Endpoints Expostos (`AlunoController`)
- **POST `/alunos`**: Cria um novo aluno.
  - **Função**: Recebe os dados de um aluno e o cadastra no sistema.
- **GET `/alunos`**: Retorna uma lista de todos os alunos.
  - **Função**: Exibe todos os alunos cadastrados.
- **GET `/alunos/{id}`**: Retorna um aluno específico, dado seu ID.
  - **Função**: Busca as informações de um aluno a partir do seu identificador único.
- **PUT `/alunos/{id}`**: Atualiza as informações de um aluno.
  - **Função**: Modifica os dados de um aluno existente.
- **DELETE `/alunos/{id}`**: Deleta um aluno do sistema.
  - **Função**: Remove um aluno a partir do seu ID.

### Swagger
A documentação da API é gerada automaticamente via Swagger, e pode ser acessada no seguinte link quando a aplicação estiver em execução:
`http://localhost:8080/swagger-ui/index.html`

---

## 4. **Anotações Utilizadas**
1. **Spring Boot**:
   - `@SpringBootApplication`: Marca a classe principal da aplicação, habilitando a configuração automática e o autoload de componentes.
   - `@RestController`: Marca uma classe como um controlador de requisições REST, simplificando a criação de APIs.
   - `@RequestMapping`: Define o caminho base para as requisições.
   - `@Service`: Identifica uma classe como um componente de serviço que contém a lógica de negócios.
   - `@Repository`: Define uma interface como responsável por interagir com o banco de dados.
   
2. **JPA**:
   - `@Entity`: Marca uma classe como uma entidade JPA que será mapeada para uma tabela do banco de dados.
   - `@Id`, `@GeneratedValue`: Define a chave primária da entidade e a estratégia de geração automática do valor (normalmente autoincremento).

3. **Lombok**:
   - `@Data`: Gera automaticamente métodos `getter`, `setter`, `toString`, `equals`, `hashCode`, e `constructor` para a classe.
   - `@NoArgsConstructor`, `@AllArgsConstructor`: Cria os construtores padrão e com todos os parâmetros.

---

## 5. **Exemplo de Fluxo**
### Cadastro de um Aluno
1. O cliente realiza um **POST** para `/alunos` com os dados do aluno no corpo da requisição.
2. O **`AlunoController`** chama o método `criarAluno` do **`AlunoService`**.
3. O **`AlunoService`** valida os dados e usa o **`AlunoRepository`** para salvar o aluno no banco de dados.
4. A resposta HTTP é retornada com o status `201 Created`, confirmando que o aluno foi cadastrado.

---

## 6. **Dependências**
- **Spring Boot**: Framework principal que facilita a construção da aplicação.
- **PostgreSQL**: Banco de dados relacional utilizado para persistência de dados.
- **Lombok**: Biblioteca que reduz a quantidade de código boilerplate, como getters e setters.
- **Spring Data JPA**: Facilita a comunicação com o banco de dados, eliminando a necessidade de implementar consultas SQL manualmente.
- **Swagger**: Ferramenta para gerar automaticamente a documentação da API REST.

---

## 7. **Descrição das Classes e Interfaces**

### `AlunoOnlineApplication.java`
- **Propósito**: Classe principal do Spring Boot. Ela inicia a aplicação e habilita a configuração automática do Spring. Contém o método `main`, que é o ponto de entrada da aplicação.
  - **Funcionamento**: O método `main` usa `SpringApplication.run(AlunoOnlineApplication.class, args)` para iniciar a aplicação.

### `AlunoController.java`
- **Propósito**: Controlador REST que gerencia as operações HTTP para a entidade `Aluno`.
  - **Funcionamento**: Usa anotações como `@RestController` para definir o controlador e `@RequestMapping` ou `@GetMapping`, `@PostMapping`, etc., para mapear as requisições HTTP aos métodos da classe.
  - **Exemplo**: O método `criarAluno()` é mapeado para o endpoint `POST /alunos`, que chama o serviço `AlunoService` para criar um novo aluno.

### `AlunoService.java`
- **Propósito**: Contém a lógica de negócios relacionada a alunos.
  - **Funcionamento**: A classe recebe chamadas dos controladores e executa a lógica de criação, atualização ou exclusão de alunos. Interage diretamente com os repositórios para manipulação dos dados.
  - **Exemplo**: O método `criarAluno()` recebe os dados de entrada, valida-os, e usa o `AlunoRepository` para salvar o aluno no banco de dados.

### `AlunoRepository.java`
- **Propósito**: Interface de persistência de dados, responsável por interagir com o banco de dados.
  - **Funcionamento**: Herda de `JpaRepository`, que fornece métodos prontos como `save()`, `findById()`, e `deleteById()`, simplificando o acesso aos dados sem a necessidade de implementação manual.
  - **Exemplo**: O método `findById()` retorna um aluno específico, dado seu ID.

### `Aluno.java`
- **Propósito**: Classe modelo que representa a entidade `Aluno`.
  - **Funcionamento**: Define os atributos do aluno e é anotada com `@Entity` para que o JPA a mapeie como uma tabela no banco de dados.
  - **Exemplo**: A classe contém campos como `id`, `nome`, `cpf`, e `email`, além de métodos `getter` e `setter` gerados automaticamente pelo Lombok.

### `SwaggerConfig.java`
- **Propósito**: Configuração do Swagger para gerar automaticamente a documentação da API.
  - **Funcionamento**: A classe configura o Swagger para que ele consiga gerar a documentação dos endpoints REST expostos no projeto, como `AlunoController`.
  - **Exemplo**: Usando a anotação `@OpenAPIDefinition`, a configuração define a versão da API e outros detalhes importantes para a documentação.

---

## 8. **Interação com o Banco de Dados e o Usuário**

### Interação com o Banco de Dados
A comunicação entre a aplicação e o banco de dados é gerida pela **Spring Data JPA**, que utiliza a **JPA (Java Persistence API)** para mapear as classes Java para tabelas no banco de dados. O fluxo de interação pode ser descrito da seguinte maneira:

1. **Modelo de Dados (Entidades)**: As classes como `Aluno` são anotadas com `@Entity` e mapeadas para tabelas no banco de dados. A JPA gerencia as operações de persistência dessas entidades.
   - **Exemplo**: A classe `Aluno.java` contém o mapeamento dos dados do aluno, como `id`, `nome`, `email`, e `cpf`.

2. **Repositórios**: As interfaces como `AlunoRepository.java` estendem `JpaRepository`, o que garante que a aplicação possa realizar operações de CRUD no banco de dados automaticamente, sem a necessidade de escrever consultas SQL complexas.
   - **Exemplo**: O repositório `AlunoRepository` define métodos como `findById()`, `save()`, e `deleteById()`, que são usados no serviço para manipular dados no banco.

3. **Serviços**: O serviço como `AlunoService` utiliza os repositórios para realizar operações no banco de dados. Ele recebe os dados dos controladores, valida e, em seguida, interage com os repositórios para salvar, atualizar ou excluir registros.
   - **Exemplo**: No método `criarAluno()`, o serviço valida os dados recebidos e os passa para o repositório para serem salvos no banco de dados.

### Interação com o Usuário
A interação com o usuário ocorre através da **API REST**, exposta pelos controladores. O processo é o seguinte:

1. **Requisição HTTP**: O cliente (usuário ou sistema externo) faz uma requisição HTTP para um endpoint da API. Exemplo: uma requisição `POST` para `/alunos` com os dados do aluno no corpo da requisição.

2. **Controlador**: O controlador, como `AlunoController`, recebe a requisição e direciona a execução para o serviço correspondente. Ele é responsável por interpretar a entrada do usuário e gerar a resposta apropriada.
   - **Exemplo**: O método `criarAluno()` do controlador mapeia a requisição `POST` para o serviço `AlunoService`, que realiza a lógica de criação.

3. **Resposta HTTP**: Após a execução da lógica no serviço, uma resposta HTTP é retornada ao cliente, com um código de status e, se necessário, dados adicionais.
   - **Exemplo**: Após a criação do aluno, o servidor retorna uma resposta `201 Created` junto com os detalhes do aluno recém-criado.

---


