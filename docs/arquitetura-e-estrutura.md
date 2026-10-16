# Arquitetura e estrutura do projeto

## 1. Objetivo

Definir uma organização inicial para o código do Passaporte dos 12 Salários, facilitando o trabalho em grupo, a manutenção e a investigação de erros. Esta estrutura é uma proposta e deve evoluir conforme o MVP for desenvolvido.

## 2. Princípios

- Uma responsabilidade principal por módulo.
- Separação entre apresentação (HTML/CSS), comportamento da tela e regras de negócio.
- Persistência local centralizada.
- Regras financeiras reutilizáveis, sem duplicação entre páginas.
- Nomes explícitos e consistentes.
- Testes para cálculos financeiros.
- Figma como referência visual e briefing como referência funcional.

## 3. Estrutura planejada

```text
/
├── index.html
├── pages/
│   ├── login.html
│   ├── boas-vindas.html
│   ├── inicio.html
│   ├── planejamento.html
│   ├── despesas.html
│   ├── metas.html
│   ├── jornada.html
│   ├── conquistas.html
│   ├── perfil.html
│   └── configuracoes.html
├── css/
│   ├── base/       # reset, variáveis de design e tipografia
│   ├── layout/     # estrutura global e responsividade
│   ├── components/ # botões, formulários, cartões, modais e potinhos
│   └── pages/      # estilos específicos de cada página
├── js/
│   ├── app.js
│   ├── config/     # constantes e configurações
│   ├── core/       # armazenamento, navegação, validações e formatadores
│   ├── modules/
│   │   ├── auth/       # login visual e onboarding
│   │   ├── salary/     # salário, planejamento e saldo
│   │   ├── pots/       # potinhos, itens e animações
│   │   ├── expenses/   # despesas e recorrências
│   │   ├── goals/      # metas e progresso
│   │   ├── habits/     # hábitos pessoais
│   │   ├── journey/    # ciclos, check-in e conquistas
│   │   └── settings/   # perfil e backup
│   ├── components/ # modais, notificações e confirmações
│   └── utils/      # moeda, datas e funções DOM
├── assets/         # imagens, ícones e fontes
├── docs/           # documentação em Markdown
└── tests/          # testes das regras principais
```

Esta é a árvore planejada, não uma declaração de que todos os arquivos já existem. Criar arquivos à medida que forem necessários, evitando arquivos vazios sem responsabilidade definida.

## 4. Responsabilidades dos módulos principais

| Módulo | Responsabilidade |
|---|---|
| `auth/login.js` | Validar campos da interface e conduzir o fluxo visual de login |
| `auth/onboarding.js` | Boas-vindas e configuração inicial |
| `salary/planning.js` | Distribuir valores planejados entre os cinco potinhos |
| `salary/balance.js` | Calcular total distribuído, valor restante e excedente |
| `pots/pots.js` | Regras gerais dos potinhos |
| `pots/items.js` | Adicionar, editar, excluir e listar itens personalizados |
| `expenses/expenses.js` | Registrar e editar despesas efetivamente realizadas |
| `expenses/recurring-expenses.js` | Periodicidade e estimativa de impacto de despesas recorrentes |
| `goals/goals.js` | Cadastro e manutenção de metas financeiras |
| `journey/salary-cycle.js` | Organização dos 12 ciclos salariais |
| `journey/monthly-checkin.js` | Reflexão e resumo mensal |
| `core/storage.js` | Persistência e recuperação centralizadas dos dados |
| `settings/backup.js` | Exportação, importação e limpeza dos dados |

## 5. Separação entre interface e regras

- HTML define a estrutura semântica da página.
- CSS controla aparência e responsividade.
- O JavaScript específico da página captura interações e atualiza a interface.
- Os módulos de domínio aplicam regras e cálculos.
- `core/storage.js` centraliza a persistência.
- `utils/` contém funções genéricas, sem depender de uma tela específica.

Evitar que cada página implemente sua própria versão do cálculo do saldo ou acesse diretamente o armazenamento com chaves diferentes.

## 6. Login e escopo do MVP

O briefing-base prevê que a primeira versão funcione sem exigir login. A tela `pages/login.html` pode ser mantida para refletir o protótipo visual, mas `auth/login.js` deve ficar restrito ao comportamento da interface até que o grupo aprove formalmente uma mudança de escopo. Não implementar autenticação real sem backend nem armazenar senhas no navegador como mecanismo seguro.

## 7. Modelo conceitual dos dados

A estrutura final deve ser confirmada junto aos requisitos e ao diagrama de classes. Como ponto de partida, separar:

- **Perfil local:** nome/apelido opcional e preferências.
- **Ciclo salarial:** número do ciclo, salário informado, datas e situação do check-in.
- **Planejamento:** distribuição planejada do ciclo.
- **Potinho:** categoria Preciso, Quero, Sonho, Protejo ou Cresço.
- **Item do potinho:** descrição e valor planejado, associado a um potinho.
- **Despesa:** descrição, valor efetivamente gasto, data e categoria.
- **Despesa recorrente:** valor, periodicidade e estado.
- **Meta financeira:** nome, valor-alvo, prazo e progresso acumulado.
- **Check-in mensal:** reflexão e comparação entre planejado e realizado.
- **Conquista:** marco comportamental atingido.

Item planejado, contribuição acumulada para uma meta e despesa são conceitos diferentes. Relacioná-los quando necessário, sem tratá-los como equivalentes.

## 8. Persistência local e backup

A aplicação deve usar uma camada central de armazenamento. Os módulos não devem espalhar acessos diretos ao `localStorage` pelo projeto. Pode-se começar com `localStorage` se os dados permanecerem simples; se a complexidade crescer, avaliar IndexedDB.

A persistência deve prever:
- tratamento de dados ausentes ou inválidos;
- identificadores estáveis para itens;
- versão do formato dos dados;
- exportação e importação de backup;
- confirmação antes de apagar ou substituir informações.

Os dados locais ficam associados ao navegador/dispositivo e não sincronizam automaticamente entre aparelhos. Limpar os dados do navegador pode removê-los.

## 9. Regras financeiras que precisam de testes

1. Comparar o total planejado com o salário informado.
2. Se o total for menor, mostrar quanto ainda falta planejar.
3. Se o total ultrapassar o salário, mostrar o excedente em linguagem acolhedora.
4. Validar valores e impedir negativos ou campos inválidos.
5. Uma despesa só entra no realizado quando for registrada como gasto.
6. Uma meta só aumenta o acumulado quando houver uma contribuição registrada.
7. Despesas recorrentes precisam de periodicidade explícita e não devem gerar duplicatas acidentais.
8. Importação de backup deve validar formato e versão antes de substituir dados.

## 10. Colaboração no GitHub

- Trabalhar em branches por funcionalidade ou documentação.
- Fazer commits pequenos e descritivos.
- Evitar duas pessoas alterando simultaneamente o mesmo arquivo.
- Combinar nomes de funções e formato dos dados entre módulos.
- Revisar a integração antes de mesclar.
- Atualizar a documentação quando uma regra ou decisão mudar.

## 11. Etapas sugeridas

1. Revisar requisitos e diagrama de classes.
2. Criar estrutura mínima e estilos globais com base no Figma.
3. Implementar armazenamento e validações centrais.
4. Implementar salário, planejamento e potinhos.
5. Implementar itens personalizados dos potinhos.
6. Implementar despesas e recorrências.
7. Implementar metas, jornada e check-in.
8. Implementar backup e configurações.
9. Testar cálculos, persistência, responsividade e integração.
