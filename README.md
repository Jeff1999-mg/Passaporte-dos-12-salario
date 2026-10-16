# Passaporte dos 12 Salários

> **Seu salário passa. O que você constrói com ele pode ficar.**

Aplicação web educativa de planejamento financeiro voltada a jovens aprendizes. O projeto busca transformar os primeiros 12 salários em uma jornada de aprendizagem: planejar, decidir, acompanhar resultados e ajustar escolhas sem julgamentos.

## Objetivo

Ajudar o jovem a compreender o destino do próprio dinheiro, distribuir o salário de acordo com sua realidade, registrar despesas, criar metas e acompanhar sua evolução durante 12 ciclos salariais.

## Funcionalidades previstas para o MVP

- Boas-vindas e configuração inicial do salário.
- Planejamento do salário entre cinco potinhos:
  - **Preciso:** necessidades e responsabilidades.
  - **Quero:** desejos e lazer.
  - **Sonho:** objetivos pessoais.
  - **Protejo:** reserva para imprevistos.
  - **Cresço:** desenvolvimento pessoal e profissional.
- Distribuição editável, com cálculo de valores e percentuais.
- Criação, edição e remoção de itens personalizados dentro dos potinhos.
- Registro de despesas realizadas e despesas recorrentes.
- Comparação entre valores planejados e realizados.
- Criação e acompanhamento de metas financeiras.
- Jornada dos 12 salários, check-in mensal e conquistas por comportamento.
- Armazenamento local, com exportação e importação de backup e opção de apagar os dados.
- Interface responsiva, com foco em celular, acessibilidade e linguagem acolhedora.

A sugestão inicial de distribuição (50% / 20% / 10% / 10% / 10%) é apenas uma referência personalizável, não uma regra universal.

## Tecnologias

- HTML
- CSS3
- JavaScript puro (Vanilla JavaScript)
- Armazenamento local no navegador
- Git e GitHub para controle de versão e colaboração
- Figma como referência visual

## Escopo e observações

O MVP foi planejado para funcionar sem exigir criação de conta. A tela de login presente no protótipo deve ser tratada como referência de interface ou fluxo futuro até que o grupo confirme uma mudança de escopo. Não implementar autenticação real nem armazenar senhas no navegador como se fosse um sistema seguro.

Os dados locais ficam associados ao navegador/dispositivo. Por isso, exportação e importação de backup fazem parte da proposta. Limpar os dados do navegador pode apagar informações locais.

## Referência visual

O Figma é a referência visual do projeto:

[Passaporte dos 12 Salários — Protótipo no Figma](https://www.figma.com/design/XFpLo4fZxgRz7ByBrPbpPy/Passaporte-dos-12-Sal%C3%A1rios-%E2%80%94-Prot%C3%B3tipo?node-id=0-1&t=k27W2QcjZfiNPQTQ-1)

Antes de alterar cores, tipografia, espaçamentos ou componentes, consultar o protótipo e os estilos definidos nele.

## Organização do repositório

```text
/
├── index.html
├── pages/                 # Uma página HTML por tela/fluxo
├── css/
│   ├── base/              # Reset, variáveis e tipografia
│   ├── layout/            # Estrutura e responsividade
│   ├── components/        # Estilos reutilizáveis
│   └── pages/             # Estilos específicos de cada tela
├── js/
│   ├── app.js             # Inicialização da aplicação
│   ├── config/            # Constantes e configurações
│   ├── core/              # Armazenamento, navegação e validações
│   ├── modules/           # Regras separadas por domínio
│   ├── components/        # Modais, notificações e confirmações
│   └── utils/             # Formatação, datas e utilitários DOM
├── assets/                # Imagens, ícones e fontes
├── docs/                  # Briefing, requisitos e diagramas em Markdown
├── tests/                 # Testes das regras principais
└── README.md
```

Essa árvore representa a organização planejada; os arquivos devem ser adicionados conforme forem implementados e revisados, sem criar arquivos vazios desnecessários.

### Responsabilidades sugeridas para os módulos

| Módulo | Responsabilidade |
|---|---|
| `auth/login.js` | Comportamento da interface de login, sem autenticação real no MVP |
| `auth/onboarding.js` | Boas-vindas e configuração inicial |
| `salary/planning.js` | Distribuição do salário entre os potinhos |
| `salary/balance.js` | Cálculo do total planejado e valor restante/excedente |
| `pots/pots.js` | Regras gerais dos cinco potinhos |
| `pots/items.js` | Adicionar, editar, remover e listar itens de cada potinho |
| `expenses/expenses.js` | Registro e manutenção de despesas realizadas |
| `expenses/recurring-expenses.js` | Regras de recorrência e impacto estimado |
| `goals/goals.js` | Cadastro e manutenção de metas financeiras |
| `journey/salary-cycle.js` | Organização dos 12 ciclos salariais |
| `journey/monthly-checkin.js` | Registro de reflexão e resumo mensal |
| `core/storage.js` | Persistência e recuperação dos dados locais |
| `settings/backup.js` | Exportação, importação e limpeza de dados |

## Regras importantes para evitar erros

1. **Separar planejamento de realização:** dinheiro planejado para uma categoria não é, por si só, uma despesa nem dinheiro já acumulado.
2. **Centralizar o armazenamento:** telas e módulos devem usar as funções de `core/storage.js), evitando chaves e formatos divergentes.
3. **Separar interface e regras:** os módulos calculam/validam dados; as páginas exibem os resultados e capturam as ações.
4. **Validar valores:** evitar valores negativos, campos vazios inválidos e somas que ultrapassem o salário sem aviso.
5. **Evitar duplicação:** funções compartilhadas, como moeda, datas e validações, ficam em `utils/` ou `core/`.
6. **Preservar os dados:** testar exportação, importação e recuperação após recarregar a página.
7. **Manter o Figma como referência:** validar cada tela em computador e celular.

## Como executar

Durante o desenvolvimento inicial, abra o repositório no VS Code e use uma extensão de servidor local, como **Live Server**, para executar as páginas. Como o projeto usa arquivos JavaScript separados, executar por um servidor local evita limitações comuns ao abrir HTML diretamente pelo caminho `file://`.

Quando a estrutura inicial estiver criada, documentaremos aqui o fluxo de execução definitivo e os testes.

## Trabalho em equipe com GitHub

- Cada pessoa deve trabalhar em uma branch para sua tarefa.
- Usar commits pequenos e descritivos.
- Atualizar a branch com as mudanças da equipe antes de integrar.
- Revisar alterações antes de mesclar.
- Evitar que duas pessoas editem o mesmo arquivo ao mesmo tempo, quando possível.
- Definir responsáveis por módulos e combinar os contratos entre eles antes de implementar integrações.

Exemplos de branches: `feature/login-ui`, `feature/pot-items`, `feature/expenses`, `docs/update-readme`.

## Documentação

Os documentos acadêmicos e técnicos devem ficar em `docs/`, em formato Markdown (`.md`), com nomes numerados e links neste README. Os documentos já produzidos devem ser preservados e adicionados ao repositório sem reescrever seus requisitos silenciosamente.

## Status

**Etapa atual:** organização da arquitetura, documentação e preparação para a implementação do MVP. A existência de telas no Figma não significa que suas funcionalidades já estejam implementadas.
