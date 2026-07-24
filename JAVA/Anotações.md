# Anotações

Java Anotações
========================

Models/Entidades -> Tabelas de Banco

DTOs -> Representação das entidades

Exceptions -> Erros personalizados

Handle -> Tratamento de exceções da nossa API

Services -> Regra de negocio

Controller -> A comunicação para API

Utils -> Métodos que serão reutilizados em vários lugares

=========================

HTTP STATUS

200 - OK
201 - Criado
204 - Sem conteúdo (delete)

400 - Erro do cliente
401 - Não autenticado
403 - Não autorizado
404 - Não encontrado
429 - Muitas requisições

500 - Erro interno do server
503 - Serviço indisponível
504 - Gateway Timeout

=======================

@SpringBootApplication 

Anotação magica do Spring boot que inicia o projeto


========================

Dependecia Lombok, facilita na criação de construtores utilizando a notação:

@RequiredArgsConstructor

Ela cria um construtor automaticamente para a sua classe. Este construtor inclui apenas campos que são declarados como final

========================

Configurações de conexão com banco de dados, são feitos no application.yaml ou application.properties

========================

Variáveis de ambiente são configurados clicando no arquivos principal que roda o projeto

Botão direito -> More Run/Debug -> Modify Run Configuration -> Modify Option -> Selecionar "Environment variables

============================

Criamos REPOSITORYs para cada Entidade do nosso banco, extendendo o JpaRepository<Entidade, Integer>

O JpaRepository cria os commando de CRUD (Criar, ler, delete e atualizar) automaticamente as entidades referenciadas.
