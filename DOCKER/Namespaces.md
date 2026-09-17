# Docker — Namespaces

## O que são Namespaces?

**Namespace** é um mecanismo do Linux utilizado pelo Docker para criar **isolamento de recursos**.

De forma simples:

> **Namespace é como uma "bolha de isolamento" que faz cada container enxergar apenas uma parte do sistema.**

Os containers continuam utilizando o mesmo **kernel Linux**, mas cada um pode ter sua própria visão de determinados recursos do sistema.

---

## Analogia simples

Imagine um prédio:

```text
                    PRÉDIO
                      │
          ┌───────────┴───────────┐
          │                       │
     APARTAMENTO A          APARTAMENTO B
          │                       │
      processos                processos
      rede                      rede
      arquivos                  arquivos
```

Os dois apartamentos estão no **mesmo prédio**, mas cada morador possui seu próprio espaço.

No Docker, é parecido:

```text
                    HOST
                      │
          ┌───────────┴───────────┐
          │                       │
      CONTAINER A            CONTAINER B
          │                       │
      processos                processos
      rede                      rede
      arquivos                 arquivos
```

Os containers compartilham o kernel do sistema, mas os **namespaces isolam a visão dos recursos**.

---

# Principais Namespaces

| Namespace | O que ele isola? | Exemplo |
|---|---|---|
| **PID** | Processos | Container possui sua própria visão dos processos |
| **NET** | Rede | Cada container possui sua própria interface e configuração de rede |
| **MNT** | Sistema de arquivos / mounts | Container possui sua própria visão dos diretórios montados |
| **UTS** | Hostname | Cada container pode possuir seu próprio hostname |
| **IPC** | Comunicação entre processos | Isola mecanismos de comunicação entre processos |
| **USER** | Usuários e IDs | Permite diferentes IDs de usuário dentro do container |

---

# 1. PID Namespace

O **PID Namespace** isola os processos.

Por exemplo:

```text
Container 1
│
├── PID 1 → minha aplicação
├── PID 2 → outro processo
└── PID 3 → outro processo
```

Enquanto outro container pode enxergar:

```text
Container 2
│
├── PID 1 → outra aplicação
├── PID 2 → outro processo
└── PID 3 → outro processo
```

O processo `PID 1` de cada container é independente dentro daquele namespace.

Isso faz com que cada container tenha sua própria visão dos processos.

---

# 2. NET Namespace

O **Network Namespace** isola a rede.

Por exemplo:

```text
Container A
└── NET Namespace
    └── 172.18.0.2

Container B
└── NET Namespace
    └── 172.18.0.3
```

Cada container possui sua própria visão das interfaces de rede, endereços IP, rotas e portas.

É uma das bases utilizadas pelo Docker para criar o isolamento de rede.

---

# 3. MNT Namespace

O **Mount Namespace** isola os pontos de montagem e a visão do sistema de arquivos.

Por exemplo:

```text
Container A
└── /
    ├── app
    ├── etc
    ├── usr
    └── var
```

Outro container pode possuir uma estrutura diferente:

```text
Container B
└── /
    ├── app
    ├── etc
    ├── usr
    └── var
```

Mesmo estando no mesmo sistema, cada container possui sua própria visão do filesystem.

---

# 4. UTS Namespace

O **UTS Namespace** permite que containers tenham diferentes **hostnames**.

```text
Container A
└── hostname: backend

Container B
└── hostname: postgres
```

Assim, cada container pode ter seu próprio nome de máquina.

---

# 5. IPC Namespace

O **IPC (Inter-Process Communication)** Namespace isola mecanismos utilizados para comunicação entre processos.

Isso impede que processos de diferentes namespaces compartilhem determinados recursos de comunicação diretamente.

De forma simples:

```text
Container A
└── processos A
    └── IPC A

Container B
└── processos B
    └── IPC B
```

---

# 6. USER Namespace

O **User Namespace** permite isolar IDs de usuários e grupos.

Por exemplo:

```text
HOST
└── usuário UID 1000

Container
└── usuário UID 0 (root)
```

O `root` dentro do container pode ser mapeado para um usuário sem privilégios no host, dependendo da configuração.

Isso ajuda a aumentar o isolamento e a segurança.

---

# Namespaces e Containers

Podemos imaginar um container assim:

```text
                    CONTAINER
                        │
        ┌───────────────┼───────────────┐
        │               │               │
      PID              NET             MNT
        │               │               │
    processos         rede          filesystem
        │               │               │
        └───────────────┼───────────────┘
                        │
                     UTS / IPC
                        │
                    isolamento
```

Cada namespace cuida de uma parte diferente do isolamento.

---

# Namespace ≠ Máquina Virtual

Essa diferença é importante.

### Máquina Virtual

```text
HOST
│
├── VM
│   ├── Sistema Operacional
│   ├── Kernel
│   └── Aplicação
│
└── VM
    ├── Sistema Operacional
    ├── Kernel
    └── Aplicação
```

Cada VM possui seu próprio **kernel**.

### Container

```text
HOST
│
└── Kernel Linux
     │
     ├── Container A
     │    └── Aplicação
     │
     └── Container B
          └── Aplicação
```

Os containers **compartilham o mesmo kernel Linux**.

Os namespaces são utilizados para criar o isolamento entre eles.

---

# Namespaces + Docker Networking

Quando usamos:

```yaml
ports:
  - "8080:80"
```

temos duas coisas diferentes acontecendo.

### 1. Network Namespace

Isola a rede do container:

```text
Container
└── Network Namespace
    └── porta 80
```

### 2. Port Publishing

O Docker publica a porta para o host:

```text
HOST :8080
     │
     ↓
DOCKER
     │
     ↓
CONTAINER :80
```

Ou seja:

```text
8080:80
│    │
│    └── Porta do container
│
└─────── Porta do host
```

Esse mecanismo é chamado de **Port Publishing** ou **Port Mapping**.

---

# Resumo

```text
Namespaces
│
├── PID  → processos
├── NET  → rede
├── MNT  → filesystem
├── UTS  → hostname
├── IPC  → comunicação entre processos
└── USER → usuários e grupos
```

A ideia principal para lembrar é:

> **Docker usa namespaces para criar isolamento entre containers.**

E:

> **Containers compartilham o kernel do host, mas possuem uma visão isolada de determinados recursos.**

### Uma frase para memorizar

**Namespace = "o que este container consegue enxergar".**

**Docker Network = "como este container se comunica".**

**Port Publishing = "como algo externo chega até o container".**