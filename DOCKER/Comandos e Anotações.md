# DOCKER

## Comandos 

**Listar Containers**: docker ps

**Baixar a imagem**: docker pull (nome da imagem)

**Iniciar Container**: docker start (id container)

**Parar Container**: docker stop (id container)

**Pausar Container**: docker pause (id container)

**Despausar Container**: docker unpause (id container)

**Rodar/Criar Container**: docker run (nome da imagem)

**Executar comando dentro do docker**: docker exec

**Mapear porta do docker no local de forma automatico**: docker run -d -P 8080:80 (id container)
**Mapear porta do docker no local de forma manual**: docker run -d -p 8080:80 (id container)

**-d**: flag detect - evita travar o console
**-P**: flag para mapeamento de porta automatico
**-p**: flag para mapeamento de porta manual
**8080:80**: a porta 8080 da minha maquina, vai se referir a porta 80 do container.]

**Finalizar e remover o container forçado**: docker rm (id container) --force

----

## Sobre Imagens

**Visualizar imagens baixadas**: docker images

**Visualizar detalhes da imagem**: docker inspect (id imagem)

**Visualizar camadas da imagem**: docker history (id imagem)


Imagens

Uma imagem é criado por camadas