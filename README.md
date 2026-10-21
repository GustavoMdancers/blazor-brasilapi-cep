# Blazor BrasilAPI CEP

Aplicação front-end em Blazor WebAssembly para consultar dados de endereços a partir de um CEP brasileiro usando a BrasilAPI.

## 📌 Sobre o projeto

Esta aplicação permite:

- consultar um CEP brasileiro;
- aceitar entradas com ou sem máscara (ex.: `01001-000` ou `01001000`);
- exibir logradouro, bairro, cidade, estado e serviço de origem;
- mostrar dados complementares do IBGE quando disponíveis;
- tratar erros de forma amigável para casos de CEP inexistente, inválido ou indisponibilidade do serviço.

A interface foi desenvolvida em Blazor, com comunicação direta com a BrasilAPI pelo cliente HTTP configurado no projeto.

## 🧩 Tecnologias utilizadas

- .NET 10
- Blazor WebAssembly
- C#
- HTML/CSS
- Bootstrap
- BrasilAPI

## 🏗️ Estrutura do projeto

```text
blazor-brasilapi-cep/
├── BlazorBrasilApiCep/
│   ├── Layout/                # Layout principal da aplicação
│   ├── Models/                # Modelos de dados da BrasilAPI
│   ├── Pages/                 # Páginas da aplicação
│   ├── Properties/            # Configurações de execução
│   ├── wwwroot/               # Assets estáticos e arquivos públicos
│   ├── App.razor              # Componente raiz da aplicação
│   ├── Program.cs             # Configuração do host e HttpClient
│   ├── _Imports.razor         # Imports globais do Blazor
│   └── BlazorBrasilApiCep.csproj
├── LICENSE
├── README.md
└── .gitignore
```

## 🚀 Pré-requisitos

Antes de executar o projeto, certifique-se de ter instalado:

- .NET SDK 10.0+
- Um navegador moderno
- Opcionalmente: VS Code com extensão C#

## ▶️ Como executar

1. Abra o terminal na pasta do projeto:

```bash
cd BlazorBrasilApiCep
```

2. Restaure os pacotes:

```bash
dotnet restore
```

3. Execute a aplicação:

```bash
dotnet run
```

4. Acesse a URL indicada no terminal, geralmente algo como:

```text
http://localhost:XXXX
```

## 🔎 Como a consulta funciona

A aplicação usa o `HttpClient` configurado com a base address da BrasilAPI:

```csharp
builder.Services.AddScoped(sp => new HttpClient
{
    BaseAddress = new Uri("https://brasilapi.com.br/")
});
```

Em seguida, a página principal faz a requisição aos endpoints:

- `cep/v1/{cep}`
- `cep/v2/{cep}` (fallback em caso de falha)

Os dados retornados são convertidos para o modelo `Cep` e exibidos na interface.

## 🧠 Fluxo de uso

1. O usuário digita um CEP;
2. o sistema remove caracteres não numéricos;
3. valida se existem 8 dígitos;
4. envia a requisição para a BrasilAPI;
5. mostra o resultado ou uma mensagem de erro amigável.

## 📝 Observações

- Esta aplicação roda no cliente (WebAssembly), ou seja, a lógica de consulta é executada no navegador.
- Caso a BrasilAPI esteja indisponível ou o CEP não exista, a aplicação exibe uma mensagem clara para o usuário.
- A aplicação foi planejada para servir como base para projetos que consomem APIs públicas de endereço no frontend em Blazor.

## 📜 Licença

Este projeto está disponível sob a licença do repositório. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.
