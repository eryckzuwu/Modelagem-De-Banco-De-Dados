# 🗄️ Modelagem de Banco de Dados — Atividades das Aulas 01 a 05

Repositório acadêmico com atividades de **Modelagem de Banco de Dados**, organizadas a partir dos conteúdos trabalhados nas aulas 01 a 05. O material reúne conceitos, levantamento de requisitos, modelagem conceitual e uma implementação prática utilizando Python e SQLite.

## 📌 Sobre o projeto

As atividades exploram diferentes etapas do desenvolvimento e da organização de bancos de dados. São trabalhados dois cenários principais:

- **Sistema de Gestão de Biblioteca**, utilizado para introduzir entidades, dados e relacionamentos e para a implementação prática com SQLite;
- **Clínica Odontológica**, utilizado no levantamento de atores, requisitos funcionais e não funcionais e regras de negócio.

## 📚 Conteúdo por aula

### Aula 01 — Introdução e conceitos iniciais

Estudo de um Sistema de Gestão de Biblioteca, identificando os principais elementos:

- **Livro:** título, ISBN, ano de publicação e autor;
- **Usuário:** nome, matrícula, e-mail e telefone;
- **Empréstimo:** data do empréstimo e data prevista de devolução.

Também são discutidos problemas que podem ocorrer sem organização dos dados, como duplicidade de cadastros, inconsistências e perda do controle dos livros emprestados.

### Aula 02 — Fundamentos, requisitos e regras de negócio

Atividades sobre:

- Diferença entre dado e informação;
- Classificação de dados estruturados e não estruturados;
- Cuidados éticos, legais e tecnológicos relacionados à LGPD;
- Minimização de dados;
- Levantamento de requisitos para uma clínica odontológica.

O cenário da clínica considera recepcionista, dentista, paciente e administrador, além de dados de pacientes, profissionais, consultas, prontuários e faturamento.

**Exemplos de requisitos levantados:**

- RF01: permitir inclusão, alteração e consulta dos dados de pacientes;
- RF02: permitir agendamentos evitando conflitos de horários;
- RF03: manter o histórico de prontuários;
- RF04: emitir relatórios financeiros por dentista e período;
- RNF01: restringir o acesso aos prontuários;
- RNF02: buscar cadastros de pacientes em menos de 2 segundos.

Também são descritas regras de negócio para bloqueio de horários, associação entre consulta, paciente e dentista, cancelamentos e preservação dos prontuários.

### Aulas 03 e 04 — Modelagem conceitual (MER/DER)

Mapeamento das entidades, atributos e relacionamentos do cenário da clínica odontológica.

**Entidades identificadas:**

- `PACIENTE`
- `DENTISTA`
- `CONSULTA`
- `PROCEDIMENTO`

A atividade identifica chaves primárias (PK), atributos e relacionamentos, incluindo:

- Paciente realiza consulta;
- Dentista atende consulta;
- Consulta inclui procedimento.

O relacionamento entre consulta e procedimento é apresentado como muitos-para-muitos (N:M).

### Aula 05 — Laboratório prático (Python + SQLite)

Implementação de um banco de dados para gestão de empréstimos de biblioteca.

O script:

1. Conecta ao banco `biblioteca.db`;
2. Habilita o suporte a chaves estrangeiras;
3. Cria as tabelas `usuario`, `livro` e `emprestimo`;
4. Insere dados de teste;
5. Consulta os empréstimos utilizando `INNER JOIN`;
6. Exibe usuário, livro, datas e status do empréstimo;
7. Encerra a conexão com o banco.

## 🧰 Tecnologias e recursos

- **Python** — linguagem utilizada no script da Aula 05;
- **SQLite** — banco de dados relacional;
- **SQL** — criação de tabelas, inserção e consulta de dados;
- **MER/DER** — modelagem conceitual;
- **LGPD** — discussão sobre proteção e tratamento de dados pessoais.

## 🗃️ Estrutura do banco de dados prático

O banco de dados da biblioteca utiliza três tabelas:

### `usuario`

| Campo | Descrição |
|---|---|
| `id_usuario` | Chave primária com incremento automático |
| `nome` | Nome do usuário |
| `email` | E-mail único e obrigatório |
| `telefone` | Telefone do usuário |

### `livro`

| Campo | Descrição |
|---|---|
| `id_livro` | Chave primária com incremento automático |
| `titulo` | Título do livro |
| `autor` | Autor do livro |
| `isbn` | ISBN único e obrigatório |

### `emprestimo`

| Campo | Descrição |
|---|---|
| `id_emprestimo` | Chave primária com incremento automático |
| `id_usuario` | Chave estrangeira relacionada a `usuario` |
| `id_livro` | Chave estrangeira relacionada a `livro` |
| `data_emprestimo` | Data do empréstimo |
| `data_devolucao` | Data da devolução |
| `status` | Situação do empréstimo, com padrão `Ativo` |

As chaves estrangeiras utilizam `ON DELETE RESTRICT`, impedindo a exclusão de registros relacionados enquanto houver empréstimos vinculados.

## ▶️ Como executar o script da Aula 05

1. Tenha o Python 3 instalado.

2. Salve o script da Aula 05 em um arquivo, por exemplo, `biblioteca.py`.

3. Abra o terminal na pasta do arquivo.

4. Execute:

```bash
python biblioteca.py
```

O módulo `sqlite3` utilizado no script faz parte da biblioteca padrão do Python. Ao executar, o programa cria o arquivo `biblioteca.db` na pasta de execução, cria as tabelas, insere os dados de teste e apresenta o relatório de empréstimos.

## 🔎 Consulta SQL utilizada

A atividade utiliza `INNER JOIN` para relacionar os empréstimos aos usuários e livros correspondentes. Também utiliza `COALESCE` para exibir `Pendente` quando a data de devolução ainda não foi preenchida.

```sql
SELECT
    e.id_emprestimo,
    u.nome AS nome_usuario,
    u.email,
    l.titulo AS titulo_livro,
    e.data_emprestimo,
    COALESCE(e.data_devolucao, 'Pendente') AS data_devolucao,
    e.status
FROM emprestimo e
INNER JOIN usuario u ON e.id_usuario = u.id_usuario
INNER JOIN livro l ON e.id_livro = l.id_livro
ORDER BY e.id_emprestimo ASC;
```

## 📂 Organização sugerida do repositório

```text
modelagem-banco-de-dados/
├── README.md
├── biblioteca.py
└── biblioteca.db
```

Os documentos das atividades e os diagramas podem ser adicionados em pastas próprias, por exemplo, `docs/` e `diagramas/`. O script Python deve ser salvo separadamente caso ainda esteja incorporado ao documento das atividades.

## 🎯 Objetivo acadêmico

Consolidar conhecimentos sobre organização de dados, requisitos, regras de negócio, modelagem conceitual, relacionamentos, chaves primárias e estrangeiras e consultas SQL. A implementação com Python e SQLite demonstra, na prática, a criação e utilização de uma estrutura relacional para controlar empréstimos de livros.
