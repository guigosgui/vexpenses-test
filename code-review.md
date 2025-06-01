# 📋 Code Review - vexpenses/backend-test

> **Legenda de prioridade**
> 🔴 `3` – Alta
> 🟡 `2` – Média
> 🟢 `1` – Baixa

---

## ⚠️ Error Handling

### 🔴 Dump
- **Arquivo**: [`app/Exceptions/Handler.php`](https://github.com/vexpenses/backend-test/blob/main/app/Exceptions/Handler.php#L136)
- **Linha**: [`136`](https://github.com/vexpenses/backend-test/blob/main/app/Exceptions/Handler.php#L136)
- **Comentário**: Não podemos subir código com `dump :D`.

### 🟡 Confusão de retorno
- **Arquivo**: [`app/UseCases/Company/Show.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/Company/Show.php#L45-L55)
- **Linha**: [`45-55`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/Company/Show.php#L45-L55)
- **Comentário**: Se o repositório retorna `null`, a exceção não será capturada e será retornado `null` para a API.

### 🟡 Sem erro
- **Arquivo**: [`app/UseCases/User/Index.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/Index.php#L75)
- **Linha**: [`75`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/Index.php#L75)
- **Comentário**: O erro não é definido corretamente.

---

## 🛠️ Reliability

### 🔴 Rota privada
- **Arquivo**: [`routes/api.php`](https://github.com/vexpenses/backend-test/blob/main/routes/api.php#L27)
- **Linha**: [`27`](https://github.com/vexpenses/backend-test/blob/main/routes/api.php#L27)
- **Comentário**: Rota está privada mesmo dentro de um grupo público.

### 🔴 Sem resposta ou tratativa
- **Arquivo**: [`app/UseCases/User/CreateFirstUser.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/CreateFirstUser.php#L68)
- **Linha**: [`68`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/CreateFirstUser.php#L68)
- **Comentário**: Sem tratamento de erro e sem testes de unidade.

### 🔴 Sem referência
- **Arquivo**: [`app/Http/Requests/Traits/SanitizesInput.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Requests/Traits/SanitizesInput.php#L56)
- **Linha**: [`56`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Requests/Traits/SanitizesInput.php#L56)
- **Comentário**: Falta referência para a classe `Sanitizer`.

### 🔴 Validação errada do método
- **Arquivo**: [`app/Http/Requests/User/UpdateRequest.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Requests/User/UpdateRequest.php#L17-L20)
- **Linha**: [`17-20`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Requests/User/UpdateRequest.php#L17-L20)
- **Comentário**: Validação falha nos parâmetros de entrada.

### 🔴 Sem validação de dados
- **Arquivo**: [`app/Http/Controllers/UserController.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L71)
- **Linha**: [`71`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L71)
- **Comentário**: Validar `request` na camada apropriada.

### 🔴 Validação de input
- **Arquivo**: [`app/Http/Controllers/CardController.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/CardController.php#L37)
- **Linha**: [`37`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/CardController.php#L37)
- **Comentário**: Necessária validação de campos externos.

---

## 🧱 Architecture

### 🔴 Acessando direto o model
- **Arquivo**: [`app/Http/Controllers/CompanyController.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/CompanyController.php#L52)
- **Linha**: [`52`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/CompanyController.php#L52)
- **Comentário**: Deveria utilizar um `Use Case`, não o model diretamente.

### 🟡 Responsabilidade / Acoplamento
- **Arquivo**: [`app/UseCases/User/CreateFirstUser.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/CreateFirstUser.php#L60)
- **Linha**: [`60`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/CreateFirstUser.php#L60)
- **Comentário**: Forte acoplamento ao validar empresa na criação do usuário.

### 🟡 Middleware com responsabilidade múltipla
- **Arquivo**: [`app/Http/Middleware/App/ResourcePolicies.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Middleware/App/ResourcePolicies.php#L42)
- **Linha**: [`42`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Middleware/App/ResourcePolicies.php#L42)
- **Comentário**: Muito acoplado e com responsabilidades mistas.

### 🟡 Injeção inversa
- **Arquivo**: [`app/Http/Controllers/UserController.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L52)
- **Linha**: [`52`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L52)
- **Comentário**: Aplicar injeção de dependência usando interfaces.

---

## 🧼 Best Practices

### 🟡 Nome nas rotas
- **Arquivo**: [`routes/api.php`](https://github.com/vexpenses/backend-test/blob/main/routes/api.php#L12)
- **Linha**: [`12`](https://github.com/vexpenses/backend-test/blob/main/routes/api.php#L12)
- **Comentário**: Nomear rotas para facilitar `redirect()->route('nome')`.

### 🟡 Parâmetro sem uso
- **Arquivo**: [`app/Http/Resources/BasePaginatorCollection.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Resources/BasePaginatorCollection.php#L10)
- **Linha**: [`10`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Resources/BasePaginatorCollection.php#L10)
- **Comentário**: `$order` não está sendo utilizado.

### 🟡 Injeção de dependência (DefaultResponse)
- **Arquivo**: [`app/Http/Controllers/UserController.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php)
- **Linhas**: [`56`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L56), [`76`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L76), [`101`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L101), [`119`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L119), [`146`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L146), [`173`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/UserController.php#L173)
- **Comentário**: Usar abstrações para facilitar testes e manutenção.

### 🟢 Middleware necessário?
- **Arquivo**: [`app/Http/Middleware/App/ResourcePolicies.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Middleware/App/ResourcePolicies.php#L15)
- **Linha**: [`15`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Middleware/App/ResourcePolicies.php#L15)
- **Comentário**: Avaliar se esse middleware é necessário, considerando os `can()` do Laravel.

---

## ⚙️ Maintainability

### 🟡 ENUM
- **Arquivo**: [`app/Domains/User/Create.php`](https://github.com/vexpenses/backend-test/blob/main/app/Domains/User/Create.php#L121)
- **Linha**: [`121`](https://github.com/vexpenses/backend-test/blob/main/app/Domains/User/Create.php#L121)
- **Comentário**: Criar `ENUM` para tipos, evita erros com valores soltos.

### 🟡 Granularidade e duplicação
- **Arquivo**: [`app/UseCases/Params/User/CreateFirstUserParams.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/Params/User/CreateFirstUserParams.php#L7)
- **Linha**: [`7`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/Params/User/CreateFirstUserParams.php#L7)
- **Comentário**: Aplicar DRY e composição de DTOs.

### 🟡 Nome da função não condiz
- **Arquivo**: [`app/UseCases/User/Create.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/Create.php#L36)
- **Linha**: [`36`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/Create.php#L36)
- **Comentário**: Função parece validar, mas está criando o usuário.

### 🟡 Injeção de dependência
- **Arquivo**: [`app/UseCases/User/Create.php`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/Create.php#L57)
- **Linha**: [`57`](https://github.com/vexpenses/backend-test/blob/main/app/UseCases/User/Create.php#L57)
- **Comentário**: Injetar dependência via construtor (mesmo sem comentário no JSON).

### 🟡 AccountController
- **Arquivo**: [`app/Http/Controllers/AccountController.php`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/AccountController.php#L74)
- **Linha**: [`74`](https://github.com/vexpenses/backend-test/blob/main/app/Http/Controllers/AccountController.php#L74)
