## Observações gerais para debate

### Arquitetura
O sistema está arquitetado baseando-se no Laravel 9, o que é bom, porém há algumas coisas que podemos oberservar e questionar sobre a arquitetura aplicada:

Considerando que a nomeclatura das pastas, e notando que temos uma pasta Domains, o sugere uma arquitetura orientada/guiada a domínios (DDD). Pensando nisso, me parece um pouco confusa a estruturação feita a partir desse paradigma.
Acredo ser mais coerente arquiteturar e organizar a pasta de Domain da seguinte forma...

    Domain/                 # Lógica de Negócio (Bounded Contexts)
    │   │   ├── AuthAndUsers/       # Contexto de Autenticação e Usuários
    │   │   │   ├── Entities/
    │   │   │   │   ├── Company.php
    │   │   │   │   └── User.php
    │   │   │   ├── Repositories/   # Podemos pensar aqui como abstrações e extensão do Eloquent
    │   │   │   │   ├── CompanyRepository.php
    │   │   │   │   └── UserRepository.php
    │   │   │   └── Services/       # Talvez não seria necessário com os Repositories (debater)
    │   │   │       ├── AuthService.php
    │   │   │       └── RegisterService.php
    │   │   ├── Accounts/             # Contexto de Contas Bancárias
    │   │   │   ├── ...
    │   │   ├── Cards/            # Contexto de Cartões
    │   │   │   ├── ...
    │   │   └── Shared/             # Talvez no futuro precisaria de algo compartilhado, como uma expansão pensando por exemplo em Agências ???
    │   │   │   ├── ...

Temos também os policies soltos na pasta. uma sugestão para melhor se adequar a uma arquitetura coesa e robusta.
Eloquent Models também, talvez ?? Debater o uso mais estrito sobre DDD separando infraestrutura ou utilizando uma adaptação Lite com a pasta app/Models

    ├── Infrastructure/
    │   ├── Persistence/
    │   │   ├── Eloquent/
    │   │   │   └── Accounts/
    │   │   │       └── EloquentAccountsRepository.php
    │   │   │   └── Models/
    │   │   │       └── AccountModel.php
    │   │   └── ...
    │   │
    │   ├── Policies/               # Nova pasta Policies no nível de infraestrutura
    │   │   ├── AccountPolicy.php   # register | block | active | show
    │   │   └── UserPolicy.php

Poderíamos ter uma infraestrutura para a integração da api/webservice. também, por fim service providers para os dominios e para a integração

    │   ├── Banking/                # Adaptações para o serviço externo BaaS
    │   │   ├── Clients/            # Clientes HTTP para a API do BaaS
    │   │   │   └── BaasHttpClient.php
    │   │   │   └── BaasAccountApiClient.php
    │   │   │   └── BaasCaredApiClient.php
    │   │   └── Services/                   # Serviços que adaptam a comunicação BaaS para o domínio
    │   │       ├── BaasAccountervice.php   # Usado pelos serviços de domínio para interagir com o BaaS
    │   │       └── BaasCaredService.php    # ...
    │   │
    │   └── Providers/          # Service Providers para registrar bindings de infraestrutura
    │       └── DomainServiceProvider.php       # Binds interfaces de domínio para implementações de infraestrutura
    │       └── BankingServiceProvider.php      # Binds serviços/clientes do BaaS / Caso mude a versão de api, instituição financeira ETC no futuro. (opcional)

### Boas práticas

Considerando boas práticas de desenvolvimento, é aconselhável:

* Criação de enums nos casos de STATUS das contas, por exemplo. Afim de podermos reaproveitar e desacoplar esses status;
* Criação de tipos específicos para transitar dados ao invés de tipos nativos (DTOs)

### Comentários:
    Comentários ao longo do projeto não são padronizados. Muitos escritos em comentários comuns e não docblocks, dificultando o entendimento do time como um todo mas também das IDE's.
    O fato de eles estarem muitos em português e outros em inglês é muito confuso e bagunçado também. Isso precisa ser padronizado.

### Readme
    O readme precisa conter informações relevantes para o desenvolvimento do projeto, como uma breve descrição do projeto, tecnologias usadas, os principais requisitos para o desenvolvimento, informações e configurações pertinentes para deploy, testes e etc.

### Docker
    Muito importante num projeto com versão desatualizada de um framework, linguagem de programação ou bibliotecas, precisa ter isso configurado de forma clara nos arquivos de configuração como composer.json, package.json etc.
    Muitas vezes, por trabalharmos em equipe diversa e em projetos diversos, acaba que perdemos muito tempo quando vamos trocar de um projeto ao outro por questões de versões e compatibilidades.
    Dessa forma, um container onde tenhamos o ambiente configurado de uma forma "fixa", garante a compatibilidade entre equipamentos e também no padrão de desenvolvimento.
    O Laravel, no caso, nos eferece o Sail, que nos ajuda, já com uma versão exata de imagens de acordo com a versão utilizada do FW. Aconselho fortemente o uso dessa ferramenta.

### Teste de Unidade
    Um sistema que se preocupa somente com testes de integração e feature, acaba deixando descobertos muitos métodos e classes; Precisamos construir testes de unidade, principalmente unidades cruciais para o funcionamento do sistema no seu core.

### DefaultResponse
    A estrutura de resposta pardão para o sistema pode gerar payload de um tamanho maior sem necessidade com informações redundantes;

    Exemplo do retorno gerado:
    {
        "success": true,
        "request": "http://localhost/api/healthcheck",
        "method": "GET",
        "code": 200,
        "data": null
    }

    Só há necessidade apresentar o nó "data", visto que todas as outras informações contidas no JSON estão no cabeçalho;

### Rota 404
    Quando jogamos uma rota inexistente na API, recebemos um código 200 com uma página exibindo uma exceção do Laravel (RouteNotFoundException).
    Devemos criar uma rota padrão para códigos de erros, principalmente 404 onde não deixemos uma mensagem crítica do sistema aparecer na tela.

### Rota Login (POST)
    Ao acessar a rota sem nenhum parâmetro de entrada, o sistema nos retorna 401 Unhauthorized, sendo que deveria expor erro 422 para validação de campos.
    Mesmo porque a rota de API está com o comentário dizendo que as rotas do grupo são públicas.
