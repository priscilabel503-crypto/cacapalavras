# Revisões internas do MVP

Este documento registra uma revisão estruturada por especialidade; não representa uma auditoria independente automatizada nem certificação de acessibilidade.

## Painel de especialistas

### 1. UX Design
- **Aprovado para protótipo:** início curto, tema visível, tabuleiro familiar, feedback imediato e caminho direto para jogar.
- **Ajuste incorporado:** seletor dos três estilos aparece fora do fluxo principal para não bloquear o início.
- **Pendente:** teste com 5–8 pessoas do público-alvo, medindo tempo até primeira tentativa, compreensão das pistas e erros de navegação.

### 2. Acessibilidade Web
- **Aprovado para revisão inicial:** HTML semântico, botão de pular para conteúdo, foco visível, operação por teclado, região `aria-live`, texto de instruções e suporte a `prefers-reduced-motion`.
- **Risco identificado:** os estados de letra ainda dependem fortemente de cores na grade; as descrições acessíveis podem ser mais explícitas para cada estado após a tentativa.
- **Pendente:** teste manual com NVDA/VoiceOver, contraste de cada combinação, zoom 200%, teclado externo e telas de 320 px. Não declarar WCAG AA sem essa validação.

### 3. Design Visual
- **Aprovado para protótipo:** três direções diferentes: A acolhedora, B editorial e C lúdica; tokens de cor e componentes compartilhados permitem comparar sem mudar a mecânica.
- **Ajuste incorporado:** opção de alternar estilo com um clique e persistência da preferência local.
- **Pendente:** validar contraste e legibilidade em dispositivos reais e escolher um único tema para o produto final.

## Revisão de conformidade com PRD

| Requisito | Estado | Observação |
|---|---|---|
| Desafio diário e tema | Parcial | Determinístico por data local, com lista de demonstração pequena |
| Até seis tentativas | Atendido | Linhas válidas até seis |
| Feedback por letra | Atendido | Trata letras repetidas consumindo ocorrências |
| Validar palavra | Parcial | Lista local limitada; não é dicionário completo |
| Resultado e solução ao final | Atendido | Revela após vitória ou derrota |
| Estatísticas e streak | Parcial | LocalStorage, sem sincronização e com poucas salvaguardas |
| Compartilhar sem revelar resposta | Atendido | Compartilha grade de emojis e número de tentativas |
| Teclado físico e virtual | Atendido | Letras, Enter e Backspace; teclado virtual por botões |
| Mobile-first | Parcial | CSS responsivo; requer validação em aparelhos reais |
| Acessibilidade | Parcial | Fundamentos incluídos; testes com leitores de tela pendentes |
| Sem cadastro/monetização | Atendido | Sem servidor nem telemetria |

## Revisão do código

- JavaScript passou pela verificação sintática `node --check`.
- A comparação de letras marca primeiro as correspondências exatas e só depois atribui letras presentes, evitando contar duplicatas acima da quantidade na solução.
- O código não faz requisições de rede; fontes externas foram removidas para manter o protótipo independente.
- **Correção recomendada antes de produção:** revisar a lista de palavras e remover itens questionáveis, ampliar o vocabulário e separar a lista de respostas da lista de palpites válidos.
- **Correção recomendada antes de produção:** fazer testes unitários automatizados para seleção diária, streak, persistência e pontuação com letras repetidas.
- **Limitação:** `localStorage` e a data local não são resistentes a alteração manual; isso é aceitável para protótipo sem conta, mas não para competição de alto risco.

## Resultado

O MVP atende o fluxo central demonstrável, mas ainda é um protótipo de validação e não uma versão de produção. Prioridades: validar a lista lexical, testar acessibilidade com tecnologias assistivas e confirmar a preferência visual antes de expandir funcionalidades.
