# Board Project

Este é um projeto Java que simula um sistema de gerenciamento de quadros (boards) com colunas e cartões (cards), incluindo funcionalidades de criação, movimentação, bloqueio e desbloqueio de cartões.

## Tecnologias Utilizadas

| Tecnologia      | Descrição                                                                                                       | Versão (se aplicável) |
| :-------------- | :-------------------------------------------------------------------------------------------------------------- | :-------------------- |
| Java            | Linguagem de programação principal.                                                               | 21                    |
| Gradle          | Ferramenta de automação de build.                                                                    | 8.8                   |
| Liquibase       | Ferramenta de controle de versão de banco de dados.                                                  | 4.29.1                |
| MySQL Connector | Driver JDBC para conexão com o banco de dados MySQL.                                                 | 8.0.33                |
| Lombok          | Biblioteca para reduzir o código boilerplate (getters, setters, construtores, etc.).                 | 1.18.34               |
| MySQL Database  | Sistema de gerenciamento de banco de dados relacional (utilizado para persistência dos dados).       | N/A                   |

## Como Usar

### Pré-requisitos

Antes de executar o projeto, certifique-se de ter o seguinte instalado:

* **JDK (Java Development Kit)**: Versão 21 ou superior. O projeto está configurado para usar o Corretto-21.
* **MySQL**: Um servidor MySQL rodando localmente.
* **Credenciais do Banco de Dados**: O projeto espera um usuário `board` com a senha `board` e um banco de dados chamado `board`. Se suas credenciais forem diferentes, você precisará modificar o arquivo `src/main/resources/liquibase.properties` e `src/main/java/br/com/dio/persistence/config/ConnectionConfig.java`.

### Configuração do Banco de Dados

O projeto utiliza o Liquibase para gerenciar as migrações do banco de dados. As migrações são executadas automaticamente na inicialização da aplicação. Certifique-se de que seu servidor MySQL esteja em execução e as credenciais estejam corretas no arquivo `liquibase.properties`.

### Executando o Projeto

1.  **Clone o repositório:** (Assumindo que o código está em um repositório Git)

    ```bash
    git clone <URL_DO_REPOSITORIO>
    cd board-39eae0975039c47420dff9fe9a09086fe112d8fa
    ```

2.  **Compile e execute:**

    Você pode compilar e executar o projeto usando o Gradle.

    No Windows:

    ```bash
    .\gradlew.bat run
    ```

    No Linux/macOS:

    ```bash
    ./gradlew run
    ```

    Ou, se você preferir compilar primeiro e depois executar o JAR:

    ```bash
    # Para compilar
    ./gradlew build

    # Para executar (o caminho do JAR pode variar dependendo da sua configuração de build)
    java -jar build/libs/Board-1.0-SNAPSHOT.jar
    ```

### Funcionalidades do Menu Principal

Ao iniciar a aplicação, você será apresentado ao `MainMenu` com as seguintes opções:

1.  **Criar um novo board**: Permite criar um novo quadro, definindo seu nome e o número de colunas adicionais (além das 3 padrão: Inicial, Final, Cancelamento). Você informará o nome para cada coluna.
2.  **Selecionar um board existente**: Permite selecionar um quadro existente pelo seu ID. Ao selecionar um quadro, você será levado ao `BoardMenu`.
3.  **Excluir um board**: Permite excluir um quadro existente pelo seu ID.
4.  **Sair**: Encerra a aplicação.

### Funcionalidades do Menu do Board

Ao selecionar um board, você entrará no `BoardMenu` com as seguintes opções:

1.  **Criar um card**: Permite criar um novo cartão, definindo seu título e descrição. O cartão será criado na coluna inicial do board.
2.  **Mover um card**: Move um cartão para a próxima coluna sequencial.
3.  **Bloquear um card**: Bloqueia um cartão, exigindo um motivo para o bloqueio. Cartões em colunas `FINAL` ou `CANCEL` não podem ser bloqueados.
4.  **Desbloquear um card**: Desbloqueia um cartão que foi previamente bloqueado.
5.  **Cancelar um card**: Move um cartão para a coluna de cancelamento.
6.  **Ver board**: Exibe os detalhes do board, incluindo suas colunas e a quantidade de cards em cada uma.
7.  **Ver coluna com cards**: Permite selecionar uma coluna e visualizar todos os cartões dentro dela, com seus títulos e descrições.
8.  **Ver card**: Exibe os detalhes de um cartão específico, incluindo se está bloqueado, o motivo do bloqueio e quantas vezes já foi bloqueado.
9.  **Voltar para o menu anterior**: Retorna ao `MainMenu`.
10. **Sair**: Encerra a aplicação.

### Tratamento de Exceções

O projeto inclui exceções personalizadas para lidar com cenários específicos, como:

* `CardBlockedException`: Lançada quando uma operação não pode ser realizada em um cartão bloqueado.
* `CardFinishedException`: Lançada quando uma operação não pode ser realizada em um cartão já finalizado.
* `EntityNotFoundException`: Lançada quando uma entidade (como um cartão ou board) não é encontrada.

---