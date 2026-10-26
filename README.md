Repositório do Projecto: Gameficado (Dashboard de Produtividade & Disciplina)

📋 Vista Geral do Projecto

Gameficado é uma plataforma web de produtividade pessoal desenvolvida numa arquitectura de ficheiro único (Single-File Architecture), focada em gerir rotinas, hábitos e objectivos através de um sistema de métricas de desempenho fiáveis.

Inspirado no conceito de gamificação comportamental (como o Habitica), o sistema substitui estéticas de fantasia RPG por uma interface sóbria estilo Workspace, utilizando conceitos como Pontos de Foco (XP), Créditos, Bateria de Disciplina e Sequências de Consistência.

🏗️ Arquitectura do Ficheiro (index.html)

A aplicação é construída sem dependências de build (sem Node.js, Webpack ou Babel) e sem frameworks reativos pesados. Toda a lógica de interface, estilos e dados reside num único ficheiro de execução nativa do navegador.

index.html
├── HTML Base & Estrutura de Abas
├── CSS Custom Properties & Design System (Estilo Workspace)
└── Script Vanilla JavaScript (IIFE Encapsulado)


Bibliotecas e Recursos Externos (CDN)

Font Awesome 6.4.0: Ícones vetoriais de interface e categorização de atributos.

Chart.js 4.4.0 (UMD): Renderização dos dashboards analíticos.

Canvas-Confetti 1.6.0: Animação de feedback tátil para conclusões e resgates.

💾 Esquema de Dados (gamification_state_v4)

Toda a informação da aplicação é armazenada no localStorage do navegador sob a chave gamification_state_v4.

{
  "attributes": [
    { "id": "attr-1", "name": "Saúde", "icon": "heartbeat", "color": "#ef4444" },
    { "id": "attr-2", "name": "Finanças", "icon": "coins", "color": "#f59e0b" }
  ],
  "tasks": [
    {
      "id": "t-1",
      "title": "Ler 15 Páginas de Livro",
      "attrId": "attr-4",
      "difficulty": "medium",
      "type": "positive",
      "recurrence": "daily",
      "customDays": [],
      "completed": false,
      "xp": 25,
      "gold": 12,
      "lastCompletedAt": null,
      "createdAt": 1700000000000
    }
  ],
  "rewards": [
    { 
      "id": "r-1", 
      "name": "1h de Entretenimento Livre", 
      "price": 50, 
      "isHpPotion": false,
      "limit": 1,
      "cycle": "weekly",
      "usedCount": 0,
      "lastResetAt": 1700000000000
    }
  ],
  "logs": [
    { "id": "l-1", "type": "system", "message": "Sistema inicializado.", "timestamp": 1700000000000 }
  ],
  "completionHistory": [
    {
      "taskId": "t-1",
      "attrId": "attr-4",
      "xp": 25,
      "gold": 12,
      "timestamp": 1700000000000
    }
  ],
  "gold": 100,
  "totalXP": 0,
  "completedCount": 0,
  "hp": 100,
  "maxHp": 100,
  "streak": 0,
  "lastStreakDate": null,
  "comebackBoostUntil": null,
  "autoBackupCounter": 0,
  "config": {
    "theme": "dark",
    "accentIndex": 0,
    "difficulties": {
      "easy": { "xp": 10, "gold": 5, "hp": 10 },
      "medium": { "xp": 25, "gold": 12, "hp": 20 },
      "hard": { "xp": 50, "gold": 25, "hp": 35 },
      "epic": { "xp": 100, "gold": 60, "hp": 50 }
    },
    "charts": {
      "xp": { "visible": true, "type": "bar" },
      "completion": { "visible": true, "type": "doughnut" },
      "evolution": { "visible": true, "type": "line" },
      "focus": { "visible": true, "type": "polarArea" }
    }
  }
}


⚙️ Funcionalidades Principais & Mecânicas

1. Visão Geral Orientada à Ação ("Missões de Hoje")

O dashboard inicial destaca prioritariamente as tarefas pendentes para o dia atual, permitindo a conclusão com um clique direto.

Abaixo das ações do dia, apresenta as estatísticas globais e a grelha de gráficos analíticos.

2. Bateria de Disciplina & Foco (Substituição Madura do HP)

Bateria de Disciplina (0 - 100%): Representa a integridade da rotina do utilizador.

Deslizes / Hábitos Negativos: Ao registar um deslize num hábito negativo, o utilizador perde uma percentagem da sua bateria e um valor correspondente de Créditos.

Restauração de Emergência: Se a bateria atingir 0%, o sistema aplica uma redução de segurança nos Créditos acumulados e restaura a bateria parcialmente para 50%.

Recarga de Energia: O utilizador pode adquirir "Recargas de Energia" na Loja para restaurar a Bateria de Disciplina através de Créditos acumulados.

3. Sequência de Consistência (Streaks) e Comeback Boost

Streak Diário (🔥): Contabiliza dias consecutivos de tarefas concluídas com validação estrita de datas.

Reset de Consistência: Se passar mais de um dia sem atividades concluídas, o streak é zerado.

Bónus de Recuperação (2x XP): Quando o streak é interrompido, o sistema ativa automaticamente um bónus de XP Dobrado durante 7 dias para incentivar o regresso imediato à rotina sem frustração.

4. Histórico Fiável de Conclusões (completionHistory)

Todas as conclusões são gravadas num vetor histórico permanente (completionHistory).

Isto garante que a reabertura de tarefas recorrentes não apaga os dados históricos dos gráficos.

5. Recorrência Automática & Personalizada

Tipos disponíveis: Única, Diária, Semanal e Personalizada (por dias da semana selecionados).

Um temporizador em segundo plano e o arranque da aplicação reiniciam automaticamente as tarefas recorrentes e os stocks de recompensas na loja.

🎨 Definições & Customização

A aba de Definições permite personalizar completamente o sistema:

Tema: Alternância instantânea entre Modo Escuro (Dark) e Modo Claro (Light).

Cor de Destaque (Accent): Escolha entre 6 cores (Azul, Verde, Roxo, Rosa, Laranja, Ciano) que atualizam as CSS variables e o theme-color do navegador.

Valores de Dificuldade: Edição dos valores de XP e Créditos para tarefas futuras.

Personalização dos Gráficos: Ocultar/exibir e alterar o tipo visual (Barra, Linha, Pizza, Rosca, Polar, Radar) para cada um dos 4 gráficos do painel.

Gestão de Dados: Exportação em CSV do histórico, exportação/importação de
