# Painel de Governança RPA

Interface web para acompanhar a execução de robôs de automação: lista de robôs, status da última
execução, histórico e logs.

> **Case técnico** desenvolvido para o processo seletivo de Auxiliar de Desenvolvimento Jr Front-End na
> **Oliveira & Antunes Advogados Associados**. O desafio era montar, do zero, a interface de
> acompanhamento dos robôs de RPA a partir de uma API de dados.

**[Ver aplicação online](https://testerpa.netlify.app/)** · React + Vite + TailwindCSS + Axios, consumindo uma API em Python

![Tela principal](docs/TelaPrincipalD.png)

## O problema

Quem opera automações precisa responder três perguntas rápido: o robô rodou, rodou quando e, se falhou,
por quê. Sem um painel, essa resposta está espalhada em logs de servidor. A proposta aqui foi reunir isso
em duas telas, em uma linguagem que um usuário não técnico entenda.

## Funcionalidades

**Tela principal**
- Listagem dos robôs em cards, com indicador visual de status
- Status e data da última execução
- Busca por nome e por status
- Layout responsivo

**Tela de detalhes**
- Dados completos do robô
- Histórico de execuções
- Consulta de logs sob demanda
- Retorno para a listagem

![Tela de detalhes](docs/DetailsD.png)

## Como executar

Requisito: Python 3.10 ou superior.

```bash
# 1. clone o repositório
git clone https://github.com/Zalone03/ProjetoOeA.git
cd ProjetoOeA

# 2. suba a API (dados fictícios, gerados na inicialização)
python servidor2.py
# a API fica em http://localhost:8000

# 3. rode o front-end
npm install
npm run dev
```

Também dá para usar a versão publicada em <https://testerpa.netlify.app/>, apontando para a API que estiver
rodando na sua máquina. Nesse caso, o navegador vai pedir permissão para acessar o localhost.

## Estrutura

```
src
├── pages
│   ├── BotsPage        lista de robôs
│   └── DetailsPage     detalhes, execuções e logs
├── components
│   ├── ui              componentes ligados aos dados (CardBot, ExecutionList, LogsList, RobotInfo)
│   └── ux              componentes reutilizáveis de interface
├── data
│   ├── api.js          instância e chamadas HTTP
│   ├── service.js      regras de acesso aos dados
│   └── Routes.jsx      rotas da aplicação
└── utils
    └── filterBots.js   filtros de busca
```

A divisão em camadas serve para que os componentes de interface não precisem conhecer detalhes da API.

## Decisões técnicas

**React + Vite**: configuração rápida e recarregamento ágil durante o desenvolvimento.

**Axios**: centraliza as chamadas HTTP em um único lugar, o que simplifica manutenção e reaproveitamento.

**TailwindCSS**: acelera ajustes de espaçamento, responsividade e alinhamento sem sair do componente.

**Cards em vez de tabela**: o enunciado falava em listagem, e comecei pensando em tabela. Nos testes, os
cards deixaram os status mais fáceis de identificar de relance e separaram melhor as informações, então
troquei.

**Componentização**: partes que começaram dentro das páginas viraram componentes próprios conforme se
repetiam: `CardBot`, `ExecutionList`, `ExecutionItem`, `LogsList` e `RobotInfo`.

## Processo de desenvolvimento

Antes de programar, rascunhei como organizar as chamadas HTTP e a estrutura de páginas, componentes e
serviços. Nem toda a sintaxe do rascunho estava certa, mas ele serviu para enxergar a estrutura antes de
escrever código.

![Organização inicial](docs/OrganizaçãoInicial.jpeg)

Primeira validação da comunicação entre o React e a API, para garantir que os dados chegavam corretos:

![Validação da API](docs/validacao1.png)

Depois vieram os ajustes de tipografia, espaçamento e alinhamento dos indicadores de status. Cheguei a
modificar o servidor temporariamente para gerar mais robôs e ver como a interface se comportava com volume:

![Teste com muitos robôs](docs/MomentosFinais+bots.png)

### Dificuldades

A maior foi decidir a fronteira entre página e componente, e onde cada responsabilidade deveria morar.
Também travei no começo com React Router e com a distribuição entre rotas e telas. Resolvi com
documentação oficial, pesquisa, e apoio de IA (ChatGPT e Gemini) para esclarecer sintaxe, discutir
alternativas de arquitetura e interpretar erros. Nada foi copiado direto para o projeto: cada sugestão foi
analisada e testada antes de entrar.

Também usei como referência: *Eloquent JavaScript*, *The Road to Learn React*, a documentação do
TailwindCSS e o freeCodeCamp.

## Melhorias futuras

- Filtros avançados por status
- Tema escuro
- Priorização dos robôs com falha
- Gráficos de acompanhamento
- Notificação de falhas
- Tratamento visual para erros capturados

## O que ficou de aprendizado

React Router, componentização, consumo de APIs REST com Axios, organização de projetos React e
TailwindCSS. Foram também os pontos em que decidi me aprofundar depois do desafio.
