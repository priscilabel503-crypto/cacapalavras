# SPECS — Implementação técnica de Palavra do Dia

## 1. Escopo e arquitetura

MVP estático sem dependências externas: `index.html` (estrutura e três propostas visuais), `styles.css` (layout responsivo e temas), `app.js` (estado, regras, persistência e interação). Pode ser aberto diretamente no navegador; não exige build ou servidor. Para implantação pública, servir por HTTPS é recomendado para APIs de compartilhamento e comportamento consistente.

## 2. Organização

- `index.html`: telas de início, jogo, resultado, estatísticas e seletor de protótipo.
- `styles.css`: tokens de cor, tipografia, componentes, três direções visuais e breakpoints.
- `app.js`: lista de palavras, seleção diária, avaliação de letras, validação, teclado, estatísticas, armazenamento e compartilhamento.
- `PRD.md`: requisitos legíveis para o desenvolvimento.
- `docs/plans/2026-10-27-jogo-casual-adivinhacao-palavras.md`: PRD versionado por data.
- `AGENTS.md`: convenções para agentes.

## 3. Modelo de dados local

Objeto persistido em `localStorage` sob chave versionada:

- `date`: data local `YYYY-MM-DD` da partida salva.
- `guesses`: lista de tentativas aceitas.
- `status`: `playing`, `won` ou `lost`.
- `stats`: `played`, `wins`, `currentStreak`, `bestStreak`, `lastCompletedDate`.

A palavra do dia não precisa ser persistida; é derivada da data e da lista de palavras. A persistência é por navegador e pode ser apagada pelo usuário.

## 4. Seleção da palavra

Converter a data local para um número inteiro de dias desde uma data-base e aplicar módulo pelo tamanho da lista de desafios. A palavra e a categoria são indexadas pela mesma posição. Isso garante determinismo local enquanto a lista e o código não mudarem. Uma versão futura deve versionar a lista e decidir explicitamente o fuso horário de publicação.

## 5. Avaliação das letras

1. Normalizar tentativa e resposta para comparação (maiúsculas e remoção de diacríticos).
2. Marcar primeiro as letras exatas na posição correta e consumir essas ocorrências.
3. Percorrer as posições restantes; marcar como presente apenas enquanto ainda houver ocorrência não consumida na resposta; caso contrário marcar ausente.
4. Atualizar o teclado sem rebaixar estado: correto > presente > ausente.

Essa ordem é necessária para lidar corretamente com letras duplicadas.

## 6. Fluxo de estado

`home` → `playing` → `won` ou `lost`. Tentativas inválidas não alteram a grade nem o contador. Uma nova data carrega o desafio correspondente. Se a partida anterior estava em andamento, ela é substituída pela nova data; o resultado concluído é contabilizado uma única vez.

## 7. Acessibilidade

- Semântica nativa e botões reais.
- `aria-live="polite"` para feedback de tentativa e `role="alert"` para erros.
- Foco visível, ordem de tabulação natural e envio por Enter.
- Estado de letra indicado por cor e símbolo/descrição textual.
- `prefers-reduced-motion` reduz animações.
- Alvos de toque amplos e layout sem dependência de hover.
- Não usar cor como único canal de informação.

## 8. Segurança e privacidade

O MVP não coleta nem envia dados para servidor. O estado permanece no navegador. A grade compartilhada contém apenas emojis/estados, nunca a palavra secreta. Não incluir analytics sem uma decisão explícita de privacidade.

## 9. Testes manuais recomendados

- Acerto na primeira tentativa e derrota após seis tentativas.
- Palavra inválida, incompleta e repetida sem gastar tentativa.
- Letras duplicadas com ocorrência única na resposta.
- Recarregar durante a partida e após conclusão.
- Virada de data e streak com dia consecutivo / dia perdido.
- Teclado físico, teclado virtual, navegação por Tab e leitor de tela.
- Larguras de 320 px, tablet e desktop; zoom de 200%.
- Preferência `prefers-reduced-motion`.
- Compartilhar/copiar sem solução.

## 10. Limitações conhecidas do protótipo

- Dicionário de demonstração pequeno; valida apenas palavras incluídas na lista local.
- Estatísticas e streak existem apenas naquele navegador.
- A data do dispositivo pode ser alterada.
- A seleção diária pode mudar se a lista de palavras for alterada entre versões.
- A acessibilidade precisa de teste real com leitores de tela e auditoria de contraste; não se declara conformidade formal.
