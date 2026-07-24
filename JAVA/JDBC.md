# JDBC

É uma API Java para acessar banco de dados relacionais

Inclui quatro componentes:

1. A API JDBC fornece programático a dados relacionais a partir da linguagem Java, usando o JDBC é possivel executar instruções SQL, recuperar resultados e enviar alterações ao banco de dados.

2. Gerenciador de Drivers JDBC: A classe DriverManager JDBC define objetos que podem conectar aplicações Java a um driver JDBC. Tradicionalmente DriverManager, tem sido a espinha dorsal da arquitetura JDBC. É bastante pequena e simples.

3. Conjunto de testes JDBC: determinam se os drivers JDBC executarão o programa.

4. Ponte JDBC-ODBC: A ponte de software Java fornece acesso JDBC por meio de drivers ODBC. O driver ODBC é mais apropriado em uma rede corporativa onde as instalações de clientes não representam um grande problema, ou para código de servidor de aplicativos escrito em Java em uma arquitetura de três camadas. 