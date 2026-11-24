<div align="center">

# 📚 Encanto Literário

**Sistema Web Administrativo para Gerenciamento de Catálogo Digital de Livros e Autores**

![PHP](https://img.shields.io/badge/PHP-8.x-777BB4?style=for-the-badge&logo=php&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-InnoDB-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![SVG](https://img.shields.io/badge/SVG-Inline-FFB13B?style=for-the-badge&logo=svg&logoColor=black)
![Status](https://img.shields.io/badge/Status-Concluído-594236?style=for-the-badge)

</div>

---

## 📖 Sobre a Encanto Literário

A **Encanto Literário** é uma livraria 100% digital que nasceu do amor pelos livros, com o propósito de aproximar leitores de grandes histórias por meio de um **catálogo digital organizado, prático e intuitivo**[cite: 7, 25].

Este repositório contém o **sistema web administrativo** desenvolvido para substituir controles manuais e planilhas estáticas por uma plataforma centralizada, segura e responsiva para a gestão completa de escritores e obras literárias[cite: 4].

### ✨ Nossa Identidade
* **🎯 Missão:** Facilitar o acesso à leitura no ambiente digital[cite: 23].
* **🔭 Visão:** Ser referência como livraria digital pela organização e experiência do cliente.
* **💛 Valores:** Paixão pela literatura, simplicidade, transparência e inovação.

---

## 🚀 Funcionalidades Principais

* **🔐 Autenticação e Controle de Sessão:** Login administrativo com senhas criptografadas em `bcrypt` (`password_hash` / `password_verify`), proteção de rotas internas (`verifica_login.php`) e criação automática do usuário padrão na inicialização[cite: 4, 15, 17, 18].
* **🧭 Painel de Navegação Rápida:** Tela inicial protegida com cartões de acesso direto aos módulos de **Autores**, **Livros** e **Catálogo Digital**[cite: 14, 16, 27].
* **✍️ Gestão de Autores (CRUD):** Cadastro, listagem alfabética, edição e exclusão de escritores (nome, gênero literário, país de origem e foto), com bloqueio de exclusão caso existam obras vinculadas (`ON DELETE RESTRICT`)[cite: 16, 19, 20].
* **📘 Gestão de Livros (CRUD):** Cadastro completo vinculado obrigatoriamente a um autor, incluindo título, editora, gênero, sinopse, capa e link externo de referência/compra[cite: 16, 20, 21].
* **🔎 Busca Dinâmica e Filtros Combináveis:** Pesquisa em tempo real por termo geral (título, editora ou autor), filtro por autor e filtro por gênero literário, com preservação dos filtros ativos após edições e alertas visuais de feedback[cite: 16, 17, 22].
* **🖼️ Processamento Automático de Mídia:** Validação real de tipo MIME (`JPG` e `PNG` até 5 MB), redimensionamento proporcional automático no servidor via **PHP GD** (`400×400 px` para autores e `400×600 px` para capas), nomes únicos (`uniqid`) e remoção física automática de arquivos antigos (`unlink`)[cite: 17, 19, 22].

---

## 🎨 Identidade Visual

A interface foi construída em **HTML5 semântico**, **CSS3 puro** (Flexbox, CSS Grid e variáveis `:root`) e ícones vetoriais **SVG inline**, utilizando uma paleta editorial quente que remete ao universo literário[cite: 10, 11]:

| Cor | Hexadecimal | Uso Principal |
| :--- | :---: | :--- |
| 🟤 **Marrom Escuro** | `#594236` | Cabeçalhos, tipografia de destaque e estrutura[cite: 11] |
| 🟡 **Dourado Envelhecido** | `#D49242` | Botões primários, detalhes e ícones[cite: 11] |
| 🟠 **Âmbar** | `#E5AC59` | Realces, *hover* e elementos secundários[cite: 11] |
| ⚪ **Bege Claro** | `#F4F1EA` | Fundo editorial suave para conforto de leitura[cite: 11] |

---

## 🛠️ Tecnologias Utilizadas

* **Front-end:** HTML5, CSS3 (`style.css` global e responsivo) e SVG inline[cite: 10, 11, 14].
* **Back-end:** PHP 8 (código modularizado, extensão `MySQLi`, extensão `GD` e expressões regulares)[cite: 14, 18].
* **Banco de Dados:** MySQL (`InnoDB`, codificação `utf8mb4_unicode_ci`) com consultas protegidas por *Prepared Statements* (`bind_param`) contra *SQL Injection*[cite: 14, 17, 19].
* **Servidor Local:** Apache (XAMPP / WAMP / Laragon)[cite: 14].
* **Metodologia:** Desenvolvimento Ágil iterativo e incremental estruturado em **2 Sprints** (Sprint 1: prototipação e UI/UX; Sprint 2: *back-end*, segurança e integração MySQL)[cite: 14].

---

## 📂 Estrutura de Arquivos

```text
Sistema_de_livros/
├── index.php              # Painel inicial protegido com cartões de acesso rápido
├── login.php              # Autenticação com verificação bcrypt
├── logout.php             # Encerramento e destruição da sessão ativa
├── verifica_login.php     # Middleware de proteção das rotas administrativas
├── conexao.php            # Conexão MySQLi (UTF-8) e inicialização do usuário padrão
├── funcoes_imagem.php     # Validação de links, upload MIME e redimensionamento (PHP GD)
├── cadastro_autores.php   # CRUD completo de autores com proteção de vínculo
├── cadastro_livros.php    # CRUD completo de livros vinculados a autores
├── biblioteca.php         # Catálogo digital com busca dinâmica e filtros combináveis
├── style.css              # Folha de estilos global, variáveis cromáticas e responsividade
└── uploads/
    ├── autores/           # Fotos dos escritores (400×400 px)
    └── capas/             # Capas dos livros (400×600 px)
```[cite: 14, 15]

---

## 🗄️ Modelagem do Banco de Dados

O banco `encanto_literario` possui três tabelas principais (`usuarios`, `autores` e `livros`), com relacionamento **1:N** entre `autores` e `livros` garantindo integridade referencial[cite: 12, 19, 20].

<details>
<summary>📄 Clique para visualizar o Script SQL (DDL)</summary>

```sql
CREATE DATABASE IF NOT EXISTS encanto_literario
CHARACTER SET utf8mb4
COLLATE utf8mb4_unicode_ci;

USE encanto_literario;

CREATE TABLE usuarios (
    id INT AUTO_INCREMENT PRIMARY KEY,
    usuario VARCHAR(50) NOT NULL UNIQUE,
    senha VARCHAR(255) NOT NULL
) ENGINE=InnoDB;

CREATE TABLE autores (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome VARCHAR(150) NOT NULL,
    genero VARCHAR(80),
    pais VARCHAR(80),
    imagem VARCHAR(255)
) ENGINE=InnoDB;

CREATE TABLE livros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    autor_id INT NOT NULL,
    titulo VARCHAR(200) NOT NULL,
    editora VARCHAR(150),
    genero VARCHAR(100),
    link_referencia VARCHAR(255) NOT NULL,
    sinopse TEXT,
    imagem_capa VARCHAR(255),
    FOREIGN KEY (autor_id) REFERENCES autores(id)
        ON DELETE RESTRICT
        ON UPDATE CASCADE
) ENGINE=InnoDB;
```

</details>[cite: 20, 21]

---

## ⚙️ Como Executar Localmente

1. **Clone o repositório** na pasta pública do seu servidor local (ex.: `htdocs/` no XAMPP):
   ```bash
   git clone [https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git](https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git)
   ```
2. **Ative o Apache e o MySQL** no painel do servidor local e certifique-se de que a extensão `gd` esteja habilitada no `php.ini`[cite: 14].
3. **Crie o banco de dados** executando o script SQL acima no phpMyAdmin ou MySQL Workbench[cite: 20, 21].
4. **Configure as credenciais** do banco em `conexao.php` (se necessário)[cite: 15].
5. **Acesse no navegador:**
   ```text
   http://localhost/Sistema_de_livros/login.php
   ```
   > 💡 Na primeira conexão, o arquivo `conexao.php` cria automaticamente o usuário `admin` padrão com senha criptografada em `bcrypt`[cite: 18, 19, 26].

---

## 🗺️ Melhorias Futuras (Roadmap)

* [ ] Implementação de múltiplos níveis de acesso (**Administrador** e **Leitor**)[cite: 22].
* [ ] Módulo de recuperação de senha por e-mail[cite: 22].
* [ ] Geração de relatórios estatísticos do catálogo digital em **PDF**[cite: 22].

---

## 👥 Equipe de Desenvolvimento

Projeto desenvolvido como Trabalho de Conclusão de Curso (TCC) no **Curso Técnico em Desenvolvimento de Sistemas** — **Escola SENAI A. Jacob Lafer** (Santo André, SP — 2026), sob orientação do **Prof. Dênis**[cite: 2, 3]
