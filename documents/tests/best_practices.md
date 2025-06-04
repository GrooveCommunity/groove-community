## ✅ Manual de Boas Práticas em Testes de Software

**"Testar cedo, testar sempre"**

### ✨ Por que seguir estas práticas?

Aqui você encontrará dicas para criar e manter uma base de testes saudável. Bons testes aumentam a confiabilidade do seu código e previnem regressões.

---

## 1. Estruture seus testes

* Separe testes unitários, de integração e end-to-end em pastas distintas.
* Use nomes descritivos para arquivos e funções de teste.

```text
src/
  components/
  tests/
    unit/
    integration/
    e2e/
```

---

## 2. Escreva testes pequenos e independentes

* Cada teste deve verificar um comportamento específico.
* Evite dependências entre testes para que possam rodar em qualquer ordem.

**Exemplo em Jest:**

```javascript
it('deve calcular o total corretamente', () => {
  const total = soma(2, 2);
  expect(total).toBe(4);
});
```

---

## 3. Mantenha o feedback rápido

* Testes lentos desestimulam execuções frequentes.
* Utilize mocks e fakes para isoar partes pesadas do sistema.

---

## 4. Automatize no CI/CD

* Configure um fluxo de integração contínua para rodar os testes a cada push ou PR.
* Exemplo simplificado com GitHub Actions:

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

---

## 5. Escreva testes legíveis

* Use descrições claras para casos de teste.
* Prefira assertivas que mostrem o comportamento esperado.

---

## 6. Atualize e remova testes obsoletos

* Tests quebrados ou desnecessários são ruídos no repositório.
* Revise periodicamente a suite para garantir relevância.

---

## 🎉 Pronto para testar!

Com estas práticas, seus testes ficarão mais úteis e fáceis de manter. Bons testes levam a um código mais confiante e robusto.
