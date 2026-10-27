# PRD — Palavra do Dia

**Data:** 2026-10-27  
**Status:** rascunho funcional para validação  
**Plataforma:** web responsiva, mobile-first  
**Público:** crianças e jovens (aprox. 8–18 anos)  
**Monetização:** nenhuma no MVP

## 1. Visão do produto

Palavra do Dia é um jogo casual diário de dedução de palavras. A pessoa tenta descobrir uma palavra secreta em até seis tentativas, recebe pistas por letra e pode consultar estatísticas e compartilhar um resumo sem revelar a solução.

## 2. Problema e objetivos

O jogo deve reduzir barreiras de entrada com regras curtas, feedback imediato e uma interface fácil de entender. Objetivo principal: incentivar retorno diário sem cadastro obrigatório. Objetivos secundários: estimular vocabulário por temas, mostrar progresso e facilitar compartilhamento voluntário.

## 3. Público e necessidades

- Pessoas que jogam principalmente pelo celular ou tablet.
- Precisam entender as regras em segundos, jogar em uma sessão curta e compreender o feedback sem depender apenas de cores.
- Persona de referência: Ana, 12 anos, gosta de desafios rápidos, temas variados e compartilhar conquistas.

## 4. Proposta de valor e ciclo principal

Uma palavra por dia, seis tentativas, tema visível, pistas por letra, resultado claro, estatísticas básicas e compartilhamento sem solução. Ciclo: abrir → ver tema → digitar tentativa → receber pistas → continuar até acertar ou esgotar tentativas → ver resultado → consultar progresso/compartilhar.

## 5. Regras de jogo

- Uma palavra diária compartilhada entre jogadores, selecionada deterministicamente pela data local do dispositivo.
- Palavras de cinco letras no MVP.
- Até seis tentativas válidas.
- Verde + símbolo/texto: letra correta na posição correta; amarelo + símbolo/texto: letra presente em outra posição; cinza + símbolo/texto: letra ausente.
- Letras repetidas são avaliadas respeitando a quantidade presente na resposta.
- Tentativas incompletas, repetidas ou fora do vocabulário permitido não consomem linha.
- Ao fim, revelar a palavra; durante a partida, não revelar a solução.
- Compartilhamento não inclui a palavra secreta.

## 6. Categorias

Prioridade do MVP: animais, comida, ciência e esportes. O conjunto de palavras deve ser adequado ao público e pode ser ampliado em futuras versões.

## 7. Funcionalidades do MVP

1. **Início:** nome, explicação curta, tema e botão para jogar.
2. **Partida:** tabuleiro 6×5, entrada por teclado físico e teclado virtual, contagem de tentativas, tema e retorno à tela inicial.
3. **Validação:** checar tamanho, repetição e lista local de palavras permitidas.
4. **Feedback:** indicar estado de cada letra e atualizar o teclado.
5. **Resultado:** vitória/derrota, palavra revelada, tentativas utilizadas e ação de reiniciar visualização/voltar ao início (o desafio diário permanece concluído).
6. **Estatísticas:** sequência atual e melhor, vitórias, partidas e percentual de acerto.
7. **Compartilhamento:** copiar texto/grade de emojis sem solução; usar compartilhamento nativo quando disponível.
8. **Persistência:** guardar estado e estatísticas no armazenamento local, sem conta.
9. **Acessibilidade:** foco visível, operação por teclado, mensagens anunciadas por leitor de tela, preferência por movimento reduzido, bom contraste e pistas que não dependam só da cor.

## 8. Requisitos funcionais

- RF01: gerar a palavra do dia de forma determinística pela data.
- RF02: associar cada palavra a uma categoria.
- RF03: validar tentativas contra a lista local.
- RF04: calcular feedback letra a letra, incluindo letras duplicadas.
- RF05: limitar a seis tentativas válidas.
- RF06: registrar vitória/derrota e estatísticas localmente.
- RF07: calcular sequência diária atual e melhor sequência.
- RF08: exibir resultado final e solução somente após o fim.
- RF09: copiar/compartilhar resultado sem revelar a solução.
- RF10: aceitar teclado físico e teclado virtual.
- RF11: funcionar em celular, tablet e desktop.
- RF12: manter progresso ao recarregar a página no mesmo navegador.

## 9. Requisitos não funcionais

- Layout mobile-first e sem rolagem horizontal em telas estreitas.
- Carregamento leve, sem bibliotecas externas obrigatórias.
- Interface em português simples, tipografia legível e alvos de toque confortáveis.
- HTML semântico e navegação por teclado.
- Sem cadastro obrigatório, monetização ou coleta de dados remotos no MVP.
- O estado é local ao navegador/dispositivo; não sincroniza entre dispositivos.

## 10. Regras de negócio

- A palavra do dia é igual para todos que usam a mesma data local e versão da lista.
- O vocabulário aceito é uma lista local limitada, não um dicionário completo de português.
- Uma tentativa válida não pode ser repetida na mesma partida.
- Uma palavra inválida deve produzir uma mensagem clara sem consumir tentativa.
- Uma partida concluída não pode ser jogada novamente no mesmo dia nesse navegador.
- O streak só avança em dias consecutivos com partida concluída; pular um dia reinicia a sequência quando uma nova partida é concluída.

## 11. Critérios de aceitação

- A tela inicial apresenta regra e tema em até duas frases curtas.
- A partida mostra seis linhas de cinco letras.
- A submissão válida atualiza feedback imediatamente.
- Palavras inválidas e tentativas repetidas não consomem linha.
- O jogo encerra ao acertar ou após seis tentativas válidas.
- A solução só aparece no resultado final.
- Estatísticas persistem após recarregar no mesmo navegador.
- O compartilhamento não expõe a solução.
- Controles essenciais são utilizáveis com teclado e toque.

## 12. Métricas sugeridas

Retenção D1/D3/D7, taxa de conclusão, taxa de vitória, média de tentativas, duração da sessão, streak médio, compartilhamentos, tentativas inválidas e tempo até a primeira tentativa. O protótipo local não envia telemetria; essas métricas exigiriam instrumentação futura com avaliação de privacidade apropriada.

## 13. Riscos e limites

- A lista de palavras é pequena e pode ser repetitiva.
- Um conjunto local de palavras não equivale a validação linguística completa.
- A data depende do relógio local e pode ser alterada pelo usuário.
- `localStorage` não oferece sincronização nem proteção contra limpeza do navegador.
- As cores e animações precisam de testes com usuários e tecnologias assistivas antes de declarar conformidade.

## 14. Fora do escopo

Ranking global, multiplayer, contas, compras, assinatura, avatares avançados, sistema complexo de recompensas, servidor e sincronização entre dispositivos.

## 15. Perguntas para a próxima iteração

1. Qual dos três estilos de protótipo deve ser a identidade visual definitiva: **A — acolhedor e colorido**, **B — minimalista editorial**, ou **C — lúdico com cartões**?
2. A palavra deve sempre ter cinco letras (recomendado para o MVP) ou você quer variar o tamanho?
3. Você prefere uma dica textual opcional por dia ou manter a dedução apenas pelo tema e pelas letras?
4. O jogo deve usar apenas palavras sem acentos no tabuleiro, normalizando acentos na validação, ou mostrar acentos quando fizerem parte da palavra?
5. O projeto final precisa continuar em HTML/CSS/JavaScript puro ou deve ser adaptado a uma stack exigida pela disciplina?

## 16. Pesquisa e referências

- Wordle / mecânica de dedução: regras de seis tentativas, feedback posicional e tratamento de letras repetidas são documentados em pesquisa acadêmica sobre o jogo. [INFORMS — Puzzle—An OR Approach for WORdle](https://pubsonline.informs.org/doi/10.1287/ited.2023.0285).
- A revisão acadêmica de Wordle discute o potencial de jogos de palavras para aprendizagem e a importância de mediação pedagógica. [SAGE — Guess the Right Word: A Review of the Language Game Wordle](https://journals.sagepub.com/doi/10.1177/00336882231192121).
- Onboarding deve ser rápido, opcional quando possível e ensinar por interação. [Apple Human Interface Guidelines — Onboarding](https://developer.apple.com/design/human-interface-guidelines/onboarding).
- Interfaces de jogos devem respeitar os métodos de interação esperados por plataforma e dimensionar controles adequadamente. [Apple — Designing for games](https://developer.apple.com/design/human-interface-guidelines/designing-for-games/).
- Orientações W3C sobre acessibilidade móvel cobrem teclado, foco e tamanho/espaçamento de alvos de toque. [W3C — Mobile Accessibility](https://www.w3.org/TR/mobile-accessibility-mapping/).
- Um exemplo de abordagem para Wordle acessível inclui anúncios de estado para leitores de tela, suporte a teclado, movimento reduzido e modos alternativos de cor. [Wordle Global — Accessibility](https://wordle.global/en/accessibility).

**Síntese da pesquisa:** o padrão de jogo funciona porque transforma cada tentativa em uma hipótese completa e o feedback em restrições para a próxima decisão. Para este público, a implementação deve explicar a mecânica rapidamente, evitar penalizar erros de digitação inválidos, comunicar pistas por mais de uma via sensorial e fazer do retorno diário uma opção convidativa, não uma pressão.
