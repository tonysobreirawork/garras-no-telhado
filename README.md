# Garras no Telhado

**Garras no Telhado** é um jogo estático de cartas para navegador, em português brasileiro, sobre gatos disputando telhados e becos durante uma noite urbana. A partida combina papéis secretos, combate por distância, cartas instantâneas, permanentes, armas, perigos, armadilhas, personagens com habilidades e adversários controlados por IA.

Todos os nomes, personagens, regras textuais, interface e elementos visuais deste projeto são originais e foram criados para este repositório.

## Como executar

1. Baixe ou clone o repositório.
2. Abra `index.html` diretamente em um navegador moderno.
3. Configure nome, quantidade de jogadores, dificuldade, velocidade, som e semente opcional.
4. Clique em **Iniciar partida**.

Não há dependências externas, backend, banco de dados, CDN, npm ou etapa de build.

## Estrutura dos arquivos

```text
index.html   Estrutura semântica da aplicação, tela inicial, mesa, mão, histórico e modais.
styles.css   Estilo responsivo, tema noturno, cartas, painéis, animações e acessibilidade visual.
script.js    Estado do jogo, catálogos, baralho, regras, IA, renderização, persistência e testes.
README.md    Este guia.
```

## Regras resumidas

- Cada partida tem 4 a 7 participantes: 1 humano e os demais controlados por IA.
- O Líder do Telhado é público; os outros papéis permanecem secretos até eliminação.
- Cada participante recebe um dos 16 gatos-personagens, sem repetição.
- O baralho tem exatamente 80 cartas, com 20 cartas de cada naipe felino: Peixe, Pata, Novelo e Lua.
- Arranhão! exige alvo vivo dentro do alcance da arma equipada.
- Salto! reage contra Arranhão!; Caixa de Papelão pode gerar defesa por verificação de Peixe.
- Armas alteram apenas o alcance, não a distância.
- Ao final do próprio turno, a mão deve ter no máximo a vida atual do jogador.
- Jogadores eliminados revelam seu papel, saem do cálculo de distância e podem conceder recompensas ou penalidades.

## Papéis

- **Líder do Telhado**: vence se permanecer vivo e não restarem Gatos de Rua nem Solitário.
- **Protetor do Beco**: vence com o Líder, ajudando a protegê-lo.
- **Gato de Rua**: vence quando o Líder é eliminado, exceto se o Solitário for o único vivo.
- **Solitário de Sete Vidas**: vence se o Líder cair quando ele for o único jogador vivo.

## Controles

- Clique em uma carta da sua mão para selecioná-la.
- Clique em **Mirar** no painel de um adversário quando a carta precisar de alvo.
- Use **Jogar carta** para confirmar.
- Use **Cancelar** para limpar seleção.
- Use **Descartar selecionadas** para cumprir descarte obrigatório ou descartar manualmente.
- Use **Encerrar turno** quando estiver em sua fase de ação e respeitando o limite de mão.
- Os botões superiores abrem regras, histórico, configurações, som, pausa da IA e reinício.

## Dificuldades da IA

- **Fácil**: mais aleatória, mas ainda respeita todas as validações.
- **Normal**: prioriza cartas úteis, alvos coerentes e conservação básica.
- **Difícil**: usa as mesmas regras de informação pública com escolhas mais consistentes e menos desperdício.

A IA recebe uma visão sanitizada do estado público por meio de `getPublicGameViewForAI`, sem acesso a papéis secretos vivos, mãos adversárias específicas ou ordem futura do baralho.

## Testes internos

Na tela inicial, abra a **Área de desenvolvimento** e clique em **Executar testes**. Também é possível abrir o console do navegador e executar:

```javascript
window.runGameTests()
```

Os testes determinísticos validam baralho, naipes, distribuição de papéis, vida inicial, distância, alcance, limites de Arranhão, regras especiais, vitória, reciclagem e semente.

## Modo de depuração

O arquivo `script.js` contém a constante:

```javascript
const DEBUG_MODE = false;
```

Para expor `window.CatRooftopDebug`, altere manualmente para `true`. Os métodos de depuração incluem inspeção de estado, execução de testes, ajuste de semente, alteração de vida, concessão de cartas, revelação de papéis e força de papel/personagem.

## Persistência

O jogo usa `localStorage` para preferências e estatísticas simples: nome, dificuldade, velocidade, som, partidas, vitórias, derrotas, dano e eliminações. Dados inválidos são ignorados sem interromper a aplicação.

## Limitações conhecidas

A interface utiliza modais próprios e IA determinística baseada em heurísticas para manter a aplicação estática e sem dependências. As ilustrações são feitas com CSS, texto e emojis Unicode, sem imagens externas.
