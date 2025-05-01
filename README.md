# 📖 Leitor de Mangá (Manga Reader)

Um site simples e funcional para o cadastro e leitura de mangás online. Este projeto tem como objetivo o aperfeiçoamento de habilidades de programação e a reestruturação de uma versão anterior criada como parte de um Trabalho de Conclusão de Curso (TCC) técnico em informática.

---

## 🧠 Objetivos do Projeto

- Praticar e melhorar conhecimentos em desenvolvimento web.
- Aplicar boas práticas de organização, estruturação de código e design.

---

## 🚀 Funcionalidades

- 📚 Cadastro de mangás (título, título-alternativo, autor, capa, sinopse, capítulos, etc.)
- 👓 Leitura online dos capítulos
- 🔍 Pesquisa de mangás por título, titulos alternativos ou autores

---

## 🛠️ Tecnologias Utilizadas

---

## 📁 Estrutura do Projeto

---

## Diretrizes de Gerenciamento

### Workflow

- Será utilizado como fluxo de trabalho padrão o [git flow](https://nvie.com/posts/a-successful-git-branching-model/);
- **main**: utilizada na hora de apresentação, base do repositório;
- **release**: branch que deve ser a mais atualizada, contado com todas as alterações de todos os devs;
- **dev**: (development) usada para produção individual. Cada desenvolvedor possui sua prórpia dev, considerando a seguinte nomenclatura para a branch -> {dev-nome_desenvolvedor}.
- **feat**: (feature) usada para produção individual. Cada desenvolvedor cria a branch a partir de sua própria dev para produzir a funcionalidade. Além disso, as branchs feat são voláteis, uma vez concluída a funcionalidade e mesclada com a respectiva dev, a branch é excluída. Considerando a seguinte nomenclatura para a branch -> {feat-nome_desenvolvedor-nome_da_feat}.
    ![alt text](https://img001.prntscr.com/file/img001/17FK2sG8R6aJwYZCELw2-g.png)

## Diretrizes de trabalho

### Pré-trabalho

- Dar _pull_ na **origin**;
- `git checkout dev-`
- Fazer _merge_ da **release** com a sua branch **dev-**, para ser possível ver as alterações mais recentes;

### Pós-trabalho

- Fazer o _commit_ e da sua **dev-**;
- Dar _pull_ na **origin**;
- Fazer _merge_ da sua branch **dev-** com a **release**;
- `git push`

### Práticas Indispensáveis

- Realizar o commit, com a seguinte forma de -m:
    ![App Screenshot](https://img001.prntscr.com/file/img001/7xcTBqHMSBezxWJm8dMETQ.png)

## Ferramentas e Recursos
