# Curso 2 - Redes: construindo um projeto com VLANs, políticas de acesso e conexão com internet

## Aula 1

======================================================================

##### LAN (Local Area Network - Rede de Área Local):

- **O que é**: Conecta dispositivos em uma área geográfica pequena e limitada, como uma casa, um escritório ou um único prédio. Ideal para compartilhar recursos localmente.

- **Exemplo**: A rede da sua casa conecta seu computador, celular e impressora ao mesmo roteador Wi-Fi.

##### MAN (Metropolitan Area Network - Rede de Área Metropolitana):

- **O que é**: Conecta várias LANs dentro de uma área geográfica maior, como uma cidade ou um campus universitário grande. Geralmente é gerenciada por uma única organização.

- **Exemplo**: A rede que interliga todos os prédios de uma universidade espalhados por diferentes bairros de uma cidade, permitindo que os alunos acessem os mesmos recursos de qualquer prédio.

##### WAN (Wide Area Network - Rede de Área Ampla):

- **O que é**: Conecta LANs e MANs que estão geograficamente muito distantes, podendo abranger cidades, países ou até continentes. É a rede de maior alcance.

- **Exemplo**: A rede de uma grande empresa multinacional que conecta seus escritórios em São Paulo, Nova York e Tóquio, permitindo que os funcionários de diferentes países colaborem e acessem os mesmos sistemas.

======================================================================

##### VLAN (Virtual Local Area Network - Redes Locais Virtuais):

- **O que é**: é uma tecnologia que permite criar redes virtuais independentes dentro de um mesmo switch físico. Dessa forma, os dispositivos são separados em grupos lógicos, impedindo que se comuniquem diretamente, o que aumenta a segurança, melhora a organização da rede e reduz o tráfego desnecessário de broadcasts.

- **Exemplo**: Uma empresa possui os departamentos de Financeiro, RH e TI, todos conectados ao mesmo switch. Sem VLAN, todos os computadores fazem parte da mesma rede e podem se comunicar entre si, o que aumenta o tráfego e pode representar um risco à segurança das informações. Ao configurar uma VLAN para cada departamento, cada um passa a fazer parte de uma rede virtual diferente. Assim, os computadores do Financeiro, por exemplo, não conseguem se comunicar diretamente com os do RH ou da TI, garantindo maior isolamento e segurança, mesmo utilizando o mesmo equipamento físico.

======================================================================

##### Protocolo DTP

O protocolo DTP (Dynamic Trunking Protocol)