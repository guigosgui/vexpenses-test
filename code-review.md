# 📋 Code Review - vexpenses/backend-test

> **Legenda de prioridade**
> 🔴 `3` – Alta
> 🟡 `2` – Média
> 🟢 `1` – Baixa

---

## ⚠️ Error Handling

### 🔴 Dump
- **Arquivo**: `app/Exceptions/Handlerphp`
- **Linha**: `136`
- **Comentário**: Não podemos subir código com `dump :D`.

### 🟡 Confusão de retorno
- **Arquivo**: `app/UseCases/Company/Show.php`
- **Linha**: `45-55`
- **Comentário**: Se o repositório retorna `null`, a exceção não será capturada e será retornado `null` para a API.

### 🟡 Sem erro
- **Arquivo**: `app/UseCases/User/Index.php`
- **Linha**: `75`
- **Comentário**: O erro não é definido corretamente.

---

## 🛠️ Reliability

### 🔴 Rota privada
- **Arquivo**: `routes/api.php`
- **Linha**: `27`
- **Comentário**: Rota está privada mesmo dentro de um grupo público.

### 🔴 Sem resposta ou tratativa
- **Arquivo**: `app/UseCases/User/CreateFirstUser.php`
- **Linha**: `68`
- **Comentário**: Sem tratamento de erro e sem testes de unidade.

### 🔴 Sem referência
- **Arquivo**: `app/Http/Requests/Traits/SanitizesInput.php`
- **Linha**: `56`
- **Comentário**: Falta referência para a classe `Sanitizer`.

### 🔴 Validação errada do método
- **Arquivo**: `app/Http/Requests/User/UpdateRequest.php`
- **Linha**: `17-20`
- **Comentário**: Validação falha nos parâmetros de entrada.

### 🔴 Sem validação de dados
- **Arquivo**: `app/Http/Controllers/UserController.php`
- **Linha**: `71`
- **Comentário**: Validar `request` na camada apropriada.

### 🔴 Validação de input
- **Arquivo**: `app/Http/Controllers/CardController.php`
- **Linha**: `37`
- **Comentário**: Necessária validação de campos externos.

---

## 🧱 Architecture

### 🔴 Acessando direto o model
- **Arquivo**: `app/Http/Controllers/CompanyController.php`
- **Linha**: `52`
- **Comentário**: Deveria utilizar um `Use Case`, não o model diretamente.

### 🟡 Responsabilidade / Acoplamento
- **Arquivo**: `app/UseCases/User/CreateFirstUser.php`
- **Linha**: `60`
- **Comentário**: Forte acoplamento ao validar empresa na criação do usuário.

### 🟡 Middleware com responsabilidade múltipla
- **Arquivo**: `app/Http/Middleware/App/ResourcePolicies.php`
- **Linha**: `42`
- **Comentário**: Muito acoplado e com responsabilidades mistas.

### 🟡 Injeção inversa
- **Arquivo**: `app/Http/Controllers/UserController.php`
- **Linha**: `52`
- **Comentário**: Aplicar injeção de dependência usando interfaces.

---

## 🧼 Best Practices

### 🟡 Nome nas rotas
- **Arquivo**: `routes/api.php`
- **Linha**: `12`
- **Comentário**: Nomear rotas para facilitar `redirect()->route('nome')`.

### 🟡 Parâmetro sem uso
- **Arquivo**: `app/Http/Resources/BasePaginatorCollection.php`
- **Linha**: `10`
- **Comentário**: `$order` não está sendo utilizado.

### 🟡 Injeção de dependência (DefaultResponse)
- **Arquivo**: `app/Http/Controllers/UserController.php`
- **Linhas**: `56, 76, 101, 119, 146, 173`
- **Comentário**: Usar abstrações para facilitar testes e manutenção.

### 🟢 Middleware necessário?
- **Arquivo**: `app/Http/Middleware/App/ResourcePolicies.php`
- **Linha**: `15`
- **Comentário**: Avaliar se esse middleware é necessário, considerando os `can()` do Laravel.

---

## ⚙️ Maintainability

### 🟡 ENUM
- **Arquivo**: `app/Domains/User/Create.php`
- **Linha**: `121`
- **Comentário**: Criar `ENUM` para tipos, evita erros com valores soltos.

### 🟡 Granularidade e duplicação
- **Arquivo**: `app/UseCases/Params/User/CreateFirstUserParams.php`
- **Linha**: `7`
- **Comentário**: Aplicar DRY e composição de DTOs.

### 🟡 Nome da função não condiz
- **Arquivo**: `app/UseCases/User/Create.php`
- **Linha**: `36`
- **Comentário**: Função parece validar, mas está criando o usuário.

### 🟡 Injeção de dependência
- **Arquivo**: `app/UseCases/User/Create.php`
- **Linha**: `57`
- **Comentário**: Injetar dependência via construtor (mesmo sem comentário no JSON).

### 🟡 AccountController
- **Arquivo**: `app/Http/Controllers/AccountController.php`
- **Linha**: `74`
- **Comentário**: Aplicar injeção de dependência.

---

## ⚖️ Separation of Concerns

### 🟡 Atribuição errada
- **Arquivo**: `app/UseCases/User/CreateFirstUser.php`
- **Linha**: `53`
- **Comentário**: Deveria validar empresa, não criá-la.

### 🟡 Nome de método inadequado
- **Arquivo**: `app/UseCases/User/CreateFirstUser.php`
- **Linha**: `78`
- **Comentário**: Nome do método sugere validação, mas realiza criação.

---

## 🌀 Complexity

### 🟡 Retorno grande e complexo
- **Arquivo**: `app/Http/Responses/DefaultResponse.php`
- **Linha**: `10`
- **Comentário**: Payload desnecessariamente grande, classe faz mais do que deveria.

---

## ✏️ Code-Style

### 🟡 Nomes genéricos
- **Arquivo**: `app/UseCases/User/show.php`
- **Linha**: `várias`
- **Comentário**: Variáveis e métodos com nomes genéricos.

### 🟡 Sometimes
- **Arquivo**: `app/Http/Requests/User/IndexRequest.php`
- **Linha**: `17-19`
- **Comentário**: Reavaliar uso de `sometimes` (doc: [laravel.com/docs/validation#validating-when-present](https://laravel.com/docs/9.x/validation#validating-when-present)).

### 🟢 Construtor fora da ordem
- **Arquivo**: `app/Repositories/Company/Find.php`
- **Linha**: `27`
- **Comentário**: Por convenção, `__construct` deve vir antes dos outros métodos.

---
