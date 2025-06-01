# Code Review Results

## [`app/Exceptions/Handler.php`](app/Exceptions/Handler.php)
### Position: `126:12-133:14`
* Priority: `0`
* Title: `Responsabilidade única`
* Category: `Separation of concerns`
* Description: `Talvez a lógica para criação de log e construção de url para o logger deveria ficar numa estrutura separada, por exemplo em infraesrtutura ou service. Não ferindo uma boa prática de responsabilidade única.`
### Position: `136:0-136:25`
* Priority: `3`
* Title: `Dump`
* Category: `Error Handling`
* Description: `Não podemos subir código com dump :D`
### Position: `136:8-136:25`
* Priority: `3`
* Title: `Dump no código`
* Category: `Reliability`
* Description: `Não podemos ter dump no código`

## [`routes/api.php`](routes/api.php)
### Position: `12:0-12:12`
* Priority: `2`
* Title: `Nome nas rotas`
* Category: `Best Practices`
* Description: `Interessante nomear as rotas para usar, por exemplo, o helper redirect()->route('profile');`
### Position: `27:0-27:85`
* Priority: `3`
* Title: `Rota privada`
* Category: `Reliability`
* Description: `Rota está privada mesmo estando dentro de um grupo publico.`

## [`app/Http/Middleware/App/ResourcePolicies.php`](app/Http/Middleware/App/ResourcePolicies.php)
### Position: `42:4-42:33`
* Priority: `2`
* Title: `Responsabilidade Unica / Alto acoplamento`
* Category: `Architecture`
* Description: `Talvez esteja muito acoplado aos controllers e também está fazendo coisas que não necessariamente são suas atribuições`

## [`app/Domains/User/Create.php`](app/Domains/User/Create.php)
### Position: `121:8-121:69`
* Priority: `2`
* Title: `ENUM`
* Category: `Maintainability`
* Description: `Ideal que seja criado um ENUM para este tipo de dado, afim de não depender deste array. Não temos como validar se o "type" está correto; O campo fica em aberto;`

## [`app/UseCases/User/CreateFirstUser.php`](app/UseCases/User/CreateFirstUser.php)
### Position: `53:3-53:61`
* Priority: `2`
* Title: `Atribuição errada`
* Category: `Separation of concerns`
* Description: `A função deveria validar a empresa e não cria-la.`
### Position: `55:16-58:9`
* Priority: `0`
* Title: `Injeção inversa`
* Category: `Architecture`
* Description: `Ideal aplicar injeção de dependência e inversão (com abstração / interface)`
### Position: `60:0-60:0`
* Priority: `2`
* Title: `Resposabilidade / Acoplamento`
* Category: `Architecture`
* Description: `Mesmo entendendo que a Empresa e Usuário são relacionados, neste caso estamos validando a empresa dentro da criação do usuário, o que gera uma forte dependência e mistura de responsabilidade`
### Position: `68:4-68:71`
* Priority: `3`
* Title: `Sem resposta ou tratativa`
* Category: `Reliability`
* Description: `Considerando que o método não retorna nada, caso haja um erro no repositorio, ele será responsável por tratar o erro, o que em essência não é ruim, porém, se acontecer um retorno diferente do esperado, por naõ ter tratativa e nem um teste de unidade, ficaremos desobertos.`
### Position: `70:26-70:62`
* Priority: `0`
* Title: `Injeção inversa`
* Category: `Architecture`
* Description: `Ideal aplicar injeção de dependência e inversão (com abstração / interface)`
### Position: `78:4-78:55`
* Priority: `2`
* Title: `Diz que faz uma e faz outra :)`
* Category: `Separation of concerns`
* Description: `Método com nome de validação que está responsável por criar.`
### Position: `123:8-123:33`
* Priority: `0`
* Title: `Erro muito abrangente`
* Category: `Reliability`
* Description: `Acredito que aqui podemos melhorar a tratativa de erro, visto que tem muitas ações a serem executadas no try e o erro abaixo é genérico.`

## [`app/Http/Responses/DefaultResponse.php`](app/Http/Responses/DefaultResponse.php)
### Position: `10:0-10:21`
* Priority: `2`
* Title: `Erro de formato/complexidade`
* Category: `Complexity`
* Description: `O retorno está muito grande, gerando payload desnecessário e redundante. A classe está muito complexa para fazer um função teoricamente simples e padronizada.`

## [`app/UseCases/Company/Show.php`](app/UseCases/Company/Show.php)
### Position: `45:7-55:0`
* Priority: `2`
* Title: `Confusão de retorno`
* Category: `Error Handling`
* Description: `Não entrei a muito fundo no repositorio e eloquent etc, porém se de lá está vindo null, como vamos capturar a exceção? Esse bloco está sendo inutilizado, certo? dessa forma pode retornar null para a api na ponta.`

## [`app/UseCases/Params/User/CreateFirstUserParams.php`](app/UseCases/Params/User/CreateFirstUserParams.php)
### Position: `7:0-7:46`
* Priority: `2`
* Title: `Granularidade e duplicação`
* Category: `Maintainability`
* Description: `Aplicar princípios como DRY e composição de DTOs. Evitar duplicação de código (repetição) e compor as classes de transfer data de forma mais coesa.`

## [`app/Http/Requests/Traits/SanitizesInput.php`](app/Http/Requests/Traits/SanitizesInput.php)
### Position: `56:8-56:69`
* Priority: `3`
* Title: `Sem referência`
* Category: `Reliability`
* Description: `Onde está a referência da Classe Sanitizer?`

## [`app/Http/Resources/BasePaginatorCollection.php`](app/Http/Resources/BasePaginatorCollection.php)
### Position: `10:0-10:64`
* Priority: `2`
* Title: `Parâmetro sem uso`
* Category: `Best Practices`
* Description: `Não há uso para $order na classe.`

## [`app/UseCases/User/Index.php`](app/UseCases/User/Index.php)
### Position: `75:1-75:33`
* Priority: `2`
* Title: `Sem erro`
* Category: `Error Handling`
* Description: `O erro não é setado chutado`

## [`app/Http/Controllers/UserController.php`](app/Http/Controllers/UserController.php)
### Position: `52:8-52:49`
* Priority: `2`
* Title: `Injeção inversa`
* Category: `Architecture`
* Description: `Ideal aplicar injeção de dependência e inversão (com abstração / interface)`
### Position: `56:16-56:32|76:16-76:32|101:16-101:32|119:16-119:32|146:16-146:32|173:16-173:32`
* Priority: `2`
* Title: `Injeção de dependência`
* Category: `Best Practices`
* Description: `Aplicar injeção de dependência, de preferencia inversa afim de usar abstrações e facilitar numa possível alteração do DefaultResponse`
### Position: `71:0-71:41`
* Priority: `3`
* Title: `Sem validação de dados`
* Category: `Reliability`
* Description: `Validar request seguindo padrão aplicado (camada de request)`

## [`app/UseCases/User/Create.php`](app/UseCases/User/Create.php)
### Position: `36:3-36:51`
* Priority: `2`
* Title: `Nome da função não condiz com sua função`
* Category: `Maintainability`
* Description: `O nome da função aponta para a responsabilidade de validar o usuário mas ela cria o usuário.`
### Position: `57:23-57:52`
* Priority: `2`
* Title: `Injeção de dependência`
* Category: `Best Practices`

## [`app/Http/Controllers/CompanyController.php`](app/Http/Controllers/CompanyController.php)
### Position: `52:8-52:80`
* Priority: `3`
* Title: `Acessando direto o model`
* Category: `Architecture`
* Description: `Deveria chamar a classe Update do domínio ou no caso, Use Case`

## [`app/UseCases/User/show.php`](app/UseCases/User/show.php)
### Position: `16:21-16:23|23:21-23:23|30:21-30:23|32:50-32:52|32:39-32:41|34:8-35:22|45:8-45:16|45:29-45:47|59:13-60:36|65:8-65:24`
* Priority: `2`
* Title: `Nomes de variáveis genéricas`
* Category: `Code-Style`
* Description: `Colocar nome dos métodos e atributos correspondentes à sua identidade`

## [`app/Http/Requests/User/UpdateRequest.php`](app/Http/Requests/User/UpdateRequest.php)
### Position: `17:11-20:70`
* Priority: `3`
* Title: `Validação errada do método`
* Category: `Reliability`
* Description: `Parametros de entrada com validação falha`

## [`app/Http/Controllers/AccountController.php`](app/Http/Controllers/AccountController.php)
### Position: `74:21-74:38`
* Priority: `2`
* Title: `Injeção de dependência`
* Category: `Maintainability`

## [`app/Http/Requests/User/IndexRequest.php`](app/Http/Requests/User/IndexRequest.php)
### Position: `17:0-19:36`
* Priority: `2`
* Title: `Sometimes remete a uma segunda validalção`
* Category: `Code-Style`
* Description: `Ver documentação sobre o tema:

https://laravel.com/docs/9.x/validation#validating-when-present`

## [`app/Http/Controllers/CardController.php`](app/Http/Controllers/CardController.php)
### Position: `37:0-37:76`
* Priority: `3`
* Title: `Validação de input`
* Category: `Reliability`
* Description: `Precisamos validar os campos que vêm de fora`
