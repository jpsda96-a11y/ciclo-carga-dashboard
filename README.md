# Ciclo & Carga — Monitorização de treino

Dashboard para acompanhar a fase do ciclo menstrual de cada atleta e ajustar carga de treino,
sincronizado com dois Google Forms (configuração do ciclo + registo diário de sintomas).

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

