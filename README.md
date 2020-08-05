# MigracaoDadosJob
Consiste em uma fluxo de importação de dados em arquivos delimitados para um banco de dados.

```
Basicamente:
Leitura de arquivo delimitado
Escrita em banco de dados JDBC
Escritor de arquivos com relatório de itens inválidos
Otimização do job - Chunk Size e Step Paralelos
```
# Configuração
Crie no seu banco de dados Mysql, duas tabelas.
1- spring_batch
2- migracao_dados
Acesse o banco de dados migracao_dados e execute esse comando abaixo.
Obs: Os arquivos que serão importados estão em um diretório no projeto "files", com dois arquivos csv, dados_bancarios.csv e pessoas.csv.
```
DROP TABLE IF EXISTS pessoa;
CREATE TABLE pessoa(id INT, nome VARCHAR(500),email VARCHAR(500),data_nascimento DATETIME,idade INT, PRIMARY KEY(id));
DROP TABLE IF EXISTS dados_bancarios;
CREATE TABLE dados_bancarios(id INT, pessoa_id INT,agencia INT, conta INT, banco INT , PRIMARY KEY(id));

```

Acesse o arquivo "application.properties" adicione a configuração da sua base de dados, caso esteja utililzando o sistema operacional Windows adicione após o seu banco de dados o "?useUnicode=true&characterEnconding=UTF-8?useTimezone=true&serverTimezone=UTC".
```
spring.datasource.jdbcUrl=jdbc:mysql://localhost:3306/spring_batch
spring.datasource.username=user
spring.datasource.password=passwrod
app.datasource.jdbcUrl=jdbc:mysql://localhost:3306/migracao_dados
app.datasource.username=user
app.datasource.password=password
spring.batch.initialize-schema=always

```
