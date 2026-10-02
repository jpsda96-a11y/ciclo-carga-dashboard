# Ciclo & Carga — Monitorização de treino

Dashboard para acompanhar a fase do ciclo menstrual de cada atleta e ajustar carga de treino,
sincronizado automaticamente a partir dos dados preenchidos pelas atletas.

## Publicar no Vercel

### Opção A — CLI (mais rápida, sem GitHub)

1. Instala o [Node.js](https://nodejs.org) se ainda não tiveres.
2. Abre o terminal **dentro desta pasta** (a que tem o `index.html`).
3. Corre:
   ```
   npx vercel
   ```
4. Segue as instruções (login no browser na primeira vez, aceita as opções por defeito).
5. No final recebes um link `https://algo.vercel.app` já ao vivo.

Para publicar atualizações futuras, corre `npx vercel --prod` na mesma pasta.

### Opção B — GitHub + import no Vercel

1. Cria um repositório novo no GitHub e faz upload do `index.html` (e deste README, opcional).
2. Vai a [vercel.com/new](https://vercel.com/new), faz login e escolhe "Import" nesse repositório.
3. Deixa as definições por defeito (é um site estático, não precisa de build) e clica em "Deploy".
4. Sempre que atualizares o ficheiro no GitHub, o Vercel republica sozinho.

## Como funciona o cálculo do ciclo

- O primeiro formulário (dados iniciais) só precisa de ser preenchido **uma vez** por atleta,
  para dar um ponto de partida (nome + estimativa inicial de duração de ciclo/período).
- A partir daí, a duração real do ciclo é calculada automaticamente a partir das respostas
  diárias à pergunta "Estás com o período hoje?" — o dashboard deteta sozinho quando cada
  período começou e ajusta a duração média, a duração do período e um aviso de "ciclo
  irregular" quando a variação entre ciclos é grande. Não é preciso voltar a preencher o
  primeiro formulário depois disso.
- Todas as atletas que constam na lista do formulário diário têm sempre um cartão próprio,
  mesmo que nunca tenham preenchido o primeiro formulário — essas atletas aparecem
  predefinidas como "ciclo irregular" (sem dados suficientes ainda) e o dashboard passa
  automaticamente para o anel/fase normal assim que acumular respostas diárias suficientes
  para calcular uma duração de ciclo fiável.

## Foto da atleta

- Em cada cartão, clica no círculo com as iniciais da atleta para carregar uma foto do
  telemóvel/computador. A imagem é recortada em quadrado e reduzida antes de ser guardada,
  para não ocupar muito espaço.

## Nota importante sobre sincronização

Este dashboard tenta sincronizar automaticamente com dois Google Sheets publicados como CSV
(configuração do ciclo e sintomas diários). Dentro do ambiente sandbox do Claude essa
sincronização automática pode estar bloqueada por restrições de rede — **depois de publicado
no Vercel, deixa de haver essa restrição**, pelo que a sincronização automática deve passar a
funcionar sozinha. Se mesmo assim houver problemas, os botões de "Carregar CSV" manual
continuam disponíveis como alternativa.

## Armazenamento de dados

- Dentro do Claude, os dados são guardados através do sistema de armazenamento partilhado do Claude.
- Fora do Claude (por exemplo, no Vercel), os dados de atletas adicionadas manualmente ficam
  guardados no `localStorage` do browser — ou seja, por dispositivo/browser, não partilhado
  automaticamente entre pessoas diferentes. Os dados sincronizados a partir do Google Forms
  continuam a ser a fonte principal e essa, sim, é igual para todos que acedam ao link.
