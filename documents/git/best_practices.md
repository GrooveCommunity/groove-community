## 🚀 Manual de Boas Práticas em Versionamento de Código (Git)

**"Pequenos Commits, Grandes Produtos"**

### ✨ Por que ler este manual?

Aqui você vai encontrar dicas práticas para usar o Git de um jeito leve, colaborativo e sem estresse. Seja você iniciante ou veterano, vale a pena conferir essas sacadas:

* Como organizar seu fluxo de trabalho sem dor de cabeça.
* Truques para manter o histórico limpo e fácil de entender.
* Ferramentas e automações que deixam tudo mais rápido.

---

## 2. Fluxo de Trabalho Leve (e Poderoso)

*Organize commits e branches para máxima clareza e eficiência.*

### 2.1 Commits que Contam Histórias

**Por quê?** Um commit bem escrito facilita

* **Navegação:** entenda rapidamente o histórico;
* **Revisão:** identifica mudanças específicas;
* **Depuração:** isola a fonte de bugs;
* **Rastreabilidade:** permite entender a intenção por trás de cada mudança.

**Exemplos Ruim vs Bom:**

* **Ruim:**

  ```bash
  git commit -m "stuff updated"
  ```
* **Bom:**

  ```bash
  git add src/components/Card.js
  git commit -m "feat(ui): nova versão do Card com sombra animada"
  ```

**Commits atômicos:** cada commit deve representar uma mudança lógica única. Isso facilita reverts, testes e leitura do histórico.

**Ferramentas úteis:**

* [GitLens (VSCode)](https://gitlens.amod.io/) (EN/PT);
* [SourceTree](https://www.sourcetreeapp.com/) (EN).

**Links de referência:**

* [Write Good Git Commit Messages](https://chris.beams.io/posts/git-commit/) (EN);
* [Como Escrever Mensagens de Commit](https://medium.com/devcast/como-escrever-mensagens-de-commit-a4e7b31fcd46) (PT).

### 2.2 Branches com Propósito

**Por quê?** Isolar trabalho evita conflitos e organiza entregas.

**Diagrama de fluxo básico:**

```text
main ←─┐
       ├─ feature/acesso-biometrico
       ├─ bugfix/overflow-no-modal
       └─ hotfix/versao-2.3.4
```

**Exemplos de nomes:**

* `feature/perfil-usuario`
* `bugfix/fix-null-pointer`
* `hotfix/v1.0.1`

**Boas práticas:**

* Atualize sua branch com `main` a cada 1–2 dias:

  ```bash
  git checkout feature/x
  git fetch origin
  git merge origin/main    # ou git rebase origin/main
  ```
* Use **rebase** para histórico linear (limpo e fácil de ler);
* Use **merge** quando quiser preservar o contexto de múltiplos commits ou quando for mais seguro em times grandes.

**Quando usar rebase vs merge:**

| Situação                                   | Rebase | Merge |
| ------------------------------------------ | ------ | ----- |
| Histórico limpo                            | ✅      | ❌     |
| Preservar contexto original                | ❌      | ✅     |
| Integração com main antes do PR            | ✅      | ❌     |
| Trabalho em equipe em branch compartilhada | ❌      | ✅     |

**Links de referência:**

* [A Successful Git Branching Model](https://nvie.com/posts/a-successful-git-branching-model/) (EN);
* [Git Flow em Português](https://medium.com/trainingcenter/utilizando-o-fluxo-git-flow-e63d5e0d5e04) (PT).

---

## 3. PRs: Hora do Checkpoint 🎯

*Transforme seus pull requests em ferramentas de alinhamento.*

**Por quê?** PRs bem estruturados:

* Garantem qualidade;
* Documentam contexto;
* Facilitam auditorias futuras.

**Template de PR (.github/PULL\_REQUEST\_TEMPLATE.md):**

```md
## O que mudou
- Listagem clara das alterações

## Por que mudamos
- Objetivo de negócio ou bug report

## Como testar
- Passo a passo para replicar

## Checklist
- [ ] Build passou
- [ ] Testes verdes
- [ ] Documentação atualizada
- [ ] Issues relacionadas linkadas (ex: Resolves #123)
```

**Dica de comunicação:**

* Marque revisores com `@equipe` para feedback rápido;
* Use labels (bug, enhancement, docs) para categorizar.

**Links de referência:**

* [GitHub PR Guides](https://docs.github.com/en/pull-requests) (EN);
* [Como Criar Pull Request](https://docs.github.com/pt/repositories) (PT).

---

## 4. Histórias Bem Escritas (Rebase & Squash)

*Deixe seu histórico polido e objetivos claros.*

**Por quê?** Histórico limpo:

* Facilita revisão retroativa;
* Minimiza commits de rascunho;
* Mantém foco no que importa.

**Antes vs Depois:**

* **Antes:** 7 commits WIP + 3 fixes;
* **Depois:** 1 commit consolidado:

  ```bash
  git rebase -i origin/main
  # marque WIP/Fix como squash
  ```

**Riscos e cuidados:**

* Nunca rebase branches já publicadas sem coordenar o time;
* Prefira **squash** em PRs abertas via GitHub:

  ```bash
  git merge --squash feature/x
  git commit -m "chore: implementa feature x"
  ```

**Links de referência:**

* [Git Rebase Documentation](https://git-scm.com/docs/git-rebase) (EN);
* [Rebase vs Merge](https://www.hostinger.com.br/tutoriais/git-rebase) (PT).

---

## 5. Mensagens de Commit com Carisma

*Conte o que, por que e como em cada mensagem.*

**Por quê?** Mensagens claras:

* Ajudam revisão e auditoria;
* Documentam decisões de design;
* Facilitam on‑boarding de novos devs.

**Formato Conventional Commits:**

```text
<tipo>(escopo?): <descrição>

[corpo opcional explicando o contexto]
```

**Tipos comuns:**

* `feat`: nova funcionalidade
* `fix`: correção de bug
* `docs`: apenas mudanças na documentação
* `style`: formatação, ponto e vírgula, etc (sem alteração de código)
* `refactor`: refatorações
* `test`: testes adicionados ou alterados
* `chore`: atualizações de build, configs, etc

**Exemplo avançado:**

```git
refactor(api): unifica validação de payload

- Remove duplicatas em auth e orders
- Simplifica tratamento de erros

Contexto: issues #345, #349 indicavam inconsistência nos endpoints.
```

**Links de referência:**

* [Conventional Commits](https://www.conventionalcommits.org) (EN/PT).

---

## 6. Deixe o Git Trabalhar por Você ⚙️

*Automatize verificações e builds para reduzir erros manuais.*

**Por quê?** Hooks e CI garantem consistência:

* **Hooks:** impedem código mal formatado;
* **CI:** valida builds e testes antes de merge;
* **Proteções:** bloqueiam commits diretos no main.

**Use ferramentas de formatação e linting:**

* [ESLint](https://eslint.org/): padroniza estilo de código JavaScript/TypeScript;
* [Prettier](https://prettier.io/): formatação automática;
* [Stylelint](https://stylelint.io/): valida estilos CSS/SASS/etc.

**Exemplo de pre-commit (.pre-commit-config.yaml):**

```yaml
repos:
  - repo: https://github.com/pre-commit/mirrors-eslint
    hooks:
      - id: eslint
```

**Exemplo GitHub Actions (.github/workflows/ci.yml):**

```yaml
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
      - run: npm ci && npm test
```

**Links de referência:**

* [pre-commit framework](https://pre-commit.com) (EN/PT);
* [GitHub Actions Guide](https://docs.github.com/en/actions) (EN/PT).

---

## 7. Extras para Times Ninja 🥷

*Práticas avançadas para elevar seu repositório ao próximo nível.*

### 7.1 Changelog Vivo

**Por quê?** Mantém histórico de releases acessível:

```md
## [1.2.0] - 2025-05-01
### Added
- Dark mode
### Fixed
- Bug no cálculo de frete
```

Links: [Keep a Changelog](https://keepachangelog.com) (EN/PT).

### 7.2 Template de Issues

```yaml
# .github/ISSUE_TEMPLATE/bug_report.yml
name: Bug report
about: Reportar um bug
title: '[BUG] '
```

Links: [Issue Templates GitHub](https://docs.github.com/en/github/building-a-strong-community) (EN/PT).

### 7.3 Segurança e Dependências

**Dependabot** (.github/dependabot.yml):

```yaml
version: 2
updates:
  - package-ecosystem: npm
    schedule: daily
```

Links: [Dependabot Docs](https://docs.github.com/en/code-security/supply-chain-security) (EN/PT).

### 7.4 Git LFS

```bash
git lfs install
git lfs track "*.psd"
```

Por quê? Evita inflar o repositório com arquivos grandes.
Links: [Git LFS](https://git-lfs.github.com) (EN/PT).

### 7.5 Onboarding Suave

**CONTRIBUTING.md**:

```md
# Como contribuir
1. git clone <url>
2. npm install
3. npm run dev
```

Por quê? Facilita a entrada de novos membros.
Links: [Contributing Guide](https://docs.github.com/en/get-started/quickstart/contributing) (EN/PT).

---

## 🎉 Você está pronto!

Cada seção foi incrementada com detalhes práticos, exemplos reais e referências bilíngues. Teste no seu projeto, compartilhe com o time e veja a produtividade subir!

**Boas commits e bons aprendizados!**
