# Guia Completo de Markdown

Markdown é uma linguagem de marcação leve. Você escreve texto simples com alguns caracteres especiais, e ele é convertido em HTML formatado. Muito usado em READMEs do GitHub, documentação, blogs e notas.

---

## 1. Cabeçalhos (Headings)

Use `#` no início da linha. Quanto mais `#`, menor o título (de H1 a H6).

```markdown
# Título 1
## Título 2
### Título 3
#### Título 4
##### Título 5
###### Título 6
```

**Resultado:**
# Título 1
## Título 2
### Título 3

> Regra: sempre coloque um espaço depois do `#`.

---

## 2. Ênfase (negrito, itálico, riscado)

| Caractere | Efeito | Exemplo | Resultado |
|---|---|---|---|
| `*texto*` ou `_texto_` | Itálico | `*urgente*` | *urgente* |
| `**texto**` ou `__texto__` | Negrito | `**urgente**` | **urgente** |
| `***texto***` | Negrito + Itálico | `***urgente***` | ***urgente*** |
| `~~texto~~` | Riscado (tachado) | `~~erro~~` | ~~erro~~ |

---

## 3. Listas

### Lista não ordenada
Use `-`, `*` ou `+` (todos funcionam igual):

```markdown
- Item 1
- Item 2
  - Subitem 2.1
  - Subitem 2.2
- Item 3
```

- Item 1
- Item 2
  - Subitem 2.1
- Item 3

### Lista ordenada
Use números seguidos de ponto:

```markdown
1. Primeiro passo
2. Segundo passo
3. Terceiro passo
```

1. Primeiro passo
2. Segundo passo

### Lista de tarefas (checklist)
Muito usada no GitHub:

```markdown
- [x] Tarefa concluída
- [ ] Tarefa pendente
```

- [x] Tarefa concluída
- [ ] Tarefa pendente

---

## 4. Links

```markdown
[Texto do link](https://exemplo.com)
[Texto com título](https://exemplo.com "Aparece ao passar o mouse")
```

Resultado: [Texto do link](https://exemplo.com)

**Link direto (autolink):**
```markdown
<https://exemplo.com>
```

---

## 5. Imagens

Igual a link, mas com `!` na frente:

```markdown
![Texto alternativo](caminho-ou-url-da-imagem.png)
```

- `!` indica que é imagem, não link.
- O texto dentro de `[]` é o **texto alternativo** (acessibilidade / aparece se a imagem não carregar).

---

## 6. Código

### Código em linha (inline)
Use crase simples `` ` ``:

```markdown
Use o comando `npm install` para instalar as dependências.
```

Resultado: Use o comando `npm install` para instalar as dependências.

### Bloco de código
Use três crases ```` ``` ```` antes e depois. Pode indicar a linguagem para colorir a sintaxe:

````markdown
```javascript
const soma = (a, b) => a + b;
console.log(soma(2, 3));
```
````

```javascript
const soma = (a, b) => a + b;
console.log(soma(2, 3));
```

---

## 7. Citações (Blockquote)

Use `>` no início da linha:

```markdown
> Isso é uma citação.
> Pode ter várias linhas.
>
> > E também pode ser aninhada.
```

> Isso é uma citação.
>
> > Citação aninhada.

---

## 8. Linha horizontal (separador)

Use três ou mais `-`, `*` ou `_` numa linha sozinha:

```markdown
---
***
___
```

Resultado:

---

## 9. Tabelas

```markdown
| Coluna 1 | Coluna 2 | Coluna 3 |
|----------|:--------:|---------:|
| esquerda | centro   | direita  |
| dado A   | dado B   | dado C   |
```

| Coluna 1 | Coluna 2 | Coluna 3 |
|----------|:--------:|---------:|
| esquerda | centro   | direita  |
| dado A   | dado B   | dado C   |

**Alinhamento nos separadores (`---`):**
- `:---` → alinha à esquerda
- `:---:` → centraliza
- `---:` → alinha à direita

---

## 10. Quebra de linha e parágrafos

- Uma linha em branco separa **parágrafos**.
- Para quebrar linha **dentro** do mesmo parágrafo, coloque **dois espaços** no final da linha (ou use `<br>`).

```markdown
Linha 1  
Linha 2 (a linha 1 termina com 2 espaços invisíveis)
```

---

## 11. Caracteres de escape

Se quiser mostrar um caractere especial sem que ele seja interpretado, use `\` antes dele:

```markdown
\*isso não vira itálico\*
\# isso não vira título
```

Resultado: \*isso não vira itálico\*

---

## 12. HTML dentro do Markdown

Markdown aceita tags HTML puras quando necessário, por exemplo:

```markdown
<sub>texto pequeno</sub>
<sup>texto sobrescrito</sup>
<br>
```

---

## 13. Notas de rodapé (nem todos os renderizadores suportam)

```markdown
Aqui vai um texto com uma nota[^1].

[^1]: Esta é a explicação da nota.
```

---

## Resumo rápido (cola de bolso)

| Símbolo | Função |
|---|---|
| `#` `##` `###` | Títulos H1, H2, H3... |
| `**texto**` | Negrito |
| `*texto*` | Itálico |
| `~~texto~~` | Riscado |
| `-` ou `*` | Lista com marcadores |
| `1.` | Lista numerada |
| `[ ]` / `[x]` | Checklist |
| `[texto](url)` | Link |
| `![texto](url)` | Imagem |
| `` `código` `` | Código inline |
| ```` ``` ```` | Bloco de código |
| `>` | Citação |
| `---` | Linha horizontal |
| `\|` | Tabelas |
| `\` | Escapar caractere especial |

---

### Dica prática para o seu projeto `rpgmaker`
Se você for documentar o backend (rotas, setup do Docker, migrações do Prisma), um bom padrão de README é:

```markdown
# Nome do Projeto

## Descrição
Breve resumo do que o projeto faz.

## Tecnologias
- Node.js / Express
- Vue 3 + TypeScript
- PostgreSQL
- Docker

## Como rodar
\`\`\`bash
docker-compose up -d
npm install
npm run dev
\`\`\`

## Estrutura de rotas
| Rota | Método | Descrição |
|---|---|---|
| /api/characters | GET | Lista personagens |
```

Isso já daria um README limpo e profissional para o repositório.
