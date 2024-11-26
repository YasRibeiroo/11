# **Documentação Técnica do Projeto Aluno Online**

## 1. **Visão Geral do Sistema**
O **Aluno Online** é uma aplicação backend criada para gerenciar informações de alunos, professores, disciplinas e matrículas em um sistema acadêmico. Utilizamos o framework **Spring Boot** para desenvolver o sistema em **Java**, e o banco de dados utilizado é o **PostgreSQL**. O sistema oferece uma interface de API RESTful que pode ser consumida por outras aplicações ou sistemas externos, com a documentação gerada automaticamente via **Swagger**.

- **Linguagem de Programação**: Java (versão 17)
- **Framework**: Spring Boot
- **Banco de Dados**: PostgreSQL
- **Gerenciador de Dependências**: Maven
- **Documentação de API**: Swagger (via SpringDoc)

---

## 2. **Estrutura do Projeto**
A estrutura do projeto foi organizada de forma a separar claramente as responsabilidades de cada parte do sistema:

### Diretórios principais:
- **`src/main/java/br/com/alunoonline/api/`**
  - **`controller/`**: Aqui ficam as classes responsáveis por definir os endpoints da API.
  - **`service/`**: Contém a lógica de negócio do sistema.
  - **`model/`**: Define as entidades (tabelas) do banco de dados.
  - **`repository/`**: As interfaces que comunicam o sistema com o banco de dados.
  - **`config/`**: Configurações extras, como o Swagger para a documentação da API.
  
- **`src/main/resources/`**
  - **`application.properties`**: Aqui ficam as configurações de ambiente, como as credenciais e URL do banco de dados.

### Componentes principais do sistema:
1. **Controller**: Responsável por receber as requisições HTTP (como GET, POST, PUT, DELETE) e chamar os serviços apropriados.
   - Exemplo: `AlunoController.java` gerencia todas as operações relacionadas aos alunos, como adicionar, editar ou remover um aluno.

2. **Service**: A lógica de negócio do sistema fica aqui. 
   - Exemplo: `AlunoService.java` contém a validação dos dados dos alunos e chama o repositório para fazer as operações no banco.

3. **Model**: Representa as entidades do banco de dados, como tabelas do PostgreSQL.
   - Exemplo: `Aluno.java` é a entidade que mapeia a tabela de alunos no banco, com campos como `id`, `nome`, `cpf` e `email`.

4. **Repository**: A comunicação com o banco de dados é feita pelas interfaces de repositório.
   - Exemplo: `AlunoRepository.java` oferece métodos prontos para interagir com a tabela de alunos, como salvar, buscar ou excluir um aluno.

---

## 3. **Funcionalidades da API**
A API expõe alguns endpoints que permitem a interação com os dados dos alunos:

- **POST `/alunos`**: Cria um novo aluno no sistema.
- **GET `/alunos`**: Retorna uma lista com todos os alunos cadastrados.
- **GET `/alunos/{id}`**: Retorna os detalhes de um aluno específico.
- **PUT `/alunos/{id}`**: Atualiza os dados de um aluno existente.
- **DELETE `/alunos/{id}`**: Exclui um aluno do sistema.

### Documentação da API com Swagger
A documentação da API é gerada automaticamente usando o Swagger, uma ferramenta muito útil para quem precisa ver e testar a API de forma interativa. Quando a aplicação estiver rodando, basta acessar:
`http://localhost:8080/swagger-ui/index.html`

---

## 4. **Anotações mais Importantes**
Aqui estão algumas anotações usadas no código e o que elas fazem:

- **Spring Boot**:
   - `@SpringBootApplication`: Marca a classe principal da aplicação, iniciando o Spring Boot e habilitando suas configurações automáticas.
   - `@RestController`: Marca a classe como responsável por tratar requisições REST, ou seja, ela recebe e responde às requisições HTTP.
   - `@RequestMapping`: Define o caminho de acesso para as requisições. Exemplo: `/alunos`.
   - `@Service`: Indica que a classe contém a lógica de negócios.
   - `@Repository`: Marca a interface que interage diretamente com o banco de dados.

- **JPA**:
   - `@Entity`: Indica que a classe é uma entidade que será mapeada para uma tabela do banco de dados.
   - `@Id`, `@GeneratedValue`: Define a chave primária da entidade e como o valor será gerado automaticamente.

- **Lombok** (para facilitar o código):
   - `@Data`: Gera automaticamente os métodos getters, setters, `toString()`, `equals()`, `hashCode()`, e o construtor.
   - `@NoArgsConstructor`, `@AllArgsConstructor`: Cria automaticamente construtores com e sem parâmetros.

---

## 5. **Fluxo de Cadastro de Aluno**
Aqui está um exemplo de como o sistema funciona quando você adiciona um novo aluno:

1. O cliente faz um **POST** para `/alunos` enviando os dados de um aluno.
2. O **AlunoController** chama o método `criarAluno()` do **AlunoService**.
3. O **AlunoService** valida os dados e chama o **AlunoRepository** para salvar o aluno no banco de dados.
4. O sistema responde com um status `201 Created`, indicando que o aluno foi criado com sucesso.

---

## 6. **Principais Dependências**
Essas são as principais bibliotecas e frameworks que usamos:

- **Spring Boot**: Facilita o desenvolvimento de aplicações Java, oferecendo uma série de funcionalidades prontas.
- **PostgreSQL**: Banco de dados relacional robusto, usado para armazenar as informações dos alunos.
- **Lombok**: Ajuda a reduzir o código repetitivo, como getters e setters.
- **Spring Data JPA**: Facilita a comunicação com o banco de dados, sem a necessidade de escrever SQL manualmente.
- **Swagger**: Gera automaticamente a documentação da API e a torna interativa, para facilitar os testes.

---

## 7. **Descrição das Classes e Interfaces**

### `AlunoOnlineApplication.java`
- **Função**: Classe principal que inicia a aplicação Spring Boot. O método `main` é o ponto de entrada do sistema e chama `SpringApplication.run()` para iniciar a aplicação.

### `AlunoController.java`
- **Função**: Responsável por definir os endpoints da API, como `POST`, `GET`, `PUT` e `DELETE`. Exemplo: o método `criarAluno()` lida com as requisições para adicionar um novo aluno.

### `AlunoService.java`
- **Função**: A lógica de negócio está aqui. Ele recebe as requisições dos controladores, valida as informações e interage com o banco de dados através do repositório.
  
### `AlunoRepository.java`
- **Função**: Interface que facilita o acesso ao banco de dados. Ela estende `JpaRepository` e fornece métodos prontos, como `findById()`, `save()`, e `delete()`.

### `Aluno.java`
- **Função**: A entidade que representa o aluno no banco de dados. Ela contém atributos como `id`, `nome`, `cpf`, e `email`, e é mapeada para a tabela de alunos no banco com a anotação `@Entity`.

---

## 8. **Como a Aplicação Interage com o Banco de Dados**

### Interação com o Banco de Dados
A comunicação com o banco é feita via **Spring Data JPA**, que usa a **JPA (Java Persistence API)** para mapear as entidades Java para as tabelas no banco de dados. O processo é simples:

1. **Modelo de Dados (Entidades)**: Classes como `Aluno` são anotadas com `@Entity` e o Spring Boot cuida de mapear essas classes para as tabelas do banco de dados.
2. **Repositórios**: Interfaces como `AlunoRepository` estendem `JpaRepository`, o que permite ao sistema realizar operações de CRUD automaticamente.
3. **Serviços**: O serviço como `AlunoService` usa os repositórios para persistir os dados. Ele recebe as entradas, valida as informações e chama o repositório para salvar ou modificar os dados no banco.

### Interação com o Usuário
1. O usuário faz uma requisição HTTP para um endpoint da API.
2. O controlador (como `AlunoController`) recebe a requisição e chama a lógica no serviço.
3. O serviço interage com o banco de dados para salvar, buscar ou excluir dados.
4. Uma resposta HTTP é devolvida ao usuário com o resultado da operação.
