## 📦 Manual de Boas Práticas para Testes em Node.js

**"Confiança em cada `npm test`"**

### ✨ Por que ler este manual?

Este guia foca em particularidades de projetos Node.js para que seus testes sejam mais eficientes e fáceis de manter.

---

## 1. Estrutura recomendada

* Separe `src/` e `tests/` ou `__tests__/` para clareza.
* Evite misturar códigos de produção e testes.

```text
my-app/
  src/
  tests/
    unit/
    integration/
```

---

## 2. Use scripts do npm

* Centralize comandos de teste no `package.json`.
* Facilite a execução com `npm test` ou `npm run test:watch`.

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch"
  }
}
```

---

## 3. Testes assíncronos

* Utilize `async/await` ou `Promises` para lidar com funções assíncronas.
* Sempre encerre testes com `await` ou retornando a `Promise` para evitar falsos positivos.

```javascript
it('deve buscar usuário do banco', async () => {
  const usuario = await repo.encontrarPorId('123');
  expect(usuario.nome).toBe('Maria');
});
```

---

## 4. Mocks e stubs

* Isole dependências externas como chamadas HTTP ou acesso a disco.
* Ferramentas populares: `jest.fn()`, `nock`, `sinon`.

```javascript
jest.mock('../servicos/email');
```

---

## 5. Cobertura de código

* Gere relatórios com `npm test -- --coverage`.
* Analise arquivos com pouca cobertura para priorizar melhorias.

---

## 6. Automatize no CI/CD

* Configure pipeline para instalar dependências e rodar testes em toda PR.
* Exemplo simplificado:

```yaml
name: node-tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm test
```

---

## 🎯 Conclusão

Seguindo estas práticas, seus projetos Node.js terão uma base de testes mais robusta e confiável. Experimente e adapte às necessidades do seu time!
