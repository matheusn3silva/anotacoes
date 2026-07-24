# Curso 1 - dos conceitos iniciais à criação de uma intranet
==================================

## Camadas (Requisição)

1. Aplicação - Protocolo HTTP 
2. Transporte (empacotar mensagem) - TCP
3. Rede (Roteador) - Protocoloco IP
4. Camada Física

Camadas (Response)

1. Camada Física
2. Rede (Roteador) - Protocoloco IP
3. Transporte (empacotar mensagem) - TCP
4. Aplicação - Protocolo HTTP


==================================

Internet utiliza protocolos (padrões) de comunicação

HTTP
TCP
UDP

==================================

A comunicação funciona entre uma solicitação e uma resposta

Requisição <<<>>> Resposta

==================================

Ping

TTL = Time-to-Live
Tempo de espera para aguardar uma resposta

==================================

Traceroute

Comando: tracert

Comando para receber a rota de trafego em um ping

==================================

**Default Gateway**: é utilizado como porta de saída das redes locais para rede externa

Faixas de octetos nos IPs
Classe A: 1 a 127

Classe B: 128 a 191

Classe C: 192 a 223

Classe D: 224 a 239 Multicast

Classe E: 240 a 255 Experimento

==================================

**CLI - Roteadores comandos**

enable -> entra no modo admin

configure terminal -> entra no terminal de configuração

? -> para abrir os possível comandos do terminal

==================================

**DHCP** - Dynamic Host Configuration Protocol

**Roteador** -> servidor DHCP

**network** -> ip da rede

**default router** -> ip do portão de saída

=====================================

### Broadcast

Ao conectar na rede, o meu smartphone realiza uma requisição broadcast (transmissão de um único ponto para muito), assim que um servidor receber essa requisição, ele me retornará um IP
