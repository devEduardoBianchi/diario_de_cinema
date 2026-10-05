# Entre Cenas — diário de cinema

Um aplicativo de portfólio feito com **HTML, CSS e JavaScript puro**. Descubra filmes, monte uma lista pessoal, registre avaliações e anotações e acompanhe sua coleção. Ele funciona de imediato com uma seleção de demonstração; a busca no catálogo do [TMDb](https://developer.themoviedb.org/docs/getting-started) é opcional.

## Como abrir

Na pasta do projeto, rode:

```powershell
py -m http.server 8000
```

Abra http://localhost:8000. Se py não estiver disponível, use python -m http.server 8000. O servidor local também mantém o armazenamento do navegador mais previsível do que abrir o arquivo diretamente.

## O que dá para fazer

- Buscar títulos na seleção de demonstração ou no catálogo do TMDb.
- Adicionar filmes à lista, marcar como vistos e editar ou remover cada registro.
- Salvar nota, data e anotação pessoal.
- Filtrar por estado e ordenar por data, título ou avaliação.
- Ver total de filmes, nota média, gêneros mais vistos e percorrer anotações do diário.

## Identidade e movimento

A direção visual chamada **Sala de projeção** usa carvão profundo, texto marfim e âmbar de projetor. A arte original do projetor foi adaptada para a abertura horizontal; o quadro da nova identidade fica em assets/ e a filosofia visual está em [design-philosophy.md](design-philosophy.md).

A tipografia combina **Fraunces** nos títulos e na marca com **Space Grotesk** nos textos e controles. As duas fontes estão incluídas localmente em `assets/fonts/`, com suas licenças SIL Open Font License.

O site continua sem etapa de compilação e não exige framework. O GSAP 3.15 e o ScrollTrigger são carregados por CDN: se a rede não estiver disponível, a interface e seus controles continuam utilizáveis, sem animação. A revelação do título como uma projeção, as entradas editoriais, o letreiro, as revelações dos cartazes e a mudança sutil de escala da imagem respeitam prefers-reduced-motion.

Os 12 filmes da coleção de demonstração usam capas provisórias servidas pelo TMDb; as imagens exigem conexão à internet. Se uma capa falhar, o cartão mostra uma composição tipográfica com o título. Os filmes buscados pela API continuam usando os cartazes retornados na busca.

O carrossel do painel apresenta somente anotações escritas pela pessoa no diário. Quando ainda não há nenhuma, o app explica como começar, em vez de exibir depoimentos inventados.

## Como ativar a busca TMDb

1. Crie uma conta no [TMDb](https://www.themoviedb.org/) e solicite acesso à API nas configurações.
2. Copie o **API Read Access Token** (o token longo de leitura, não a chave curta).
3. Abra **Configurar catálogo**, cole o token e selecione **Ativar catálogo**.

O token é enviado no cabeçalho Authorization: Bearer ... e fica no sessionStorage, apenas durante a sessão da aba. Ele não aparece no código. A coleção pessoal fica no localStorage, neste navegador, sem sincronização ou conta de usuário.

Uma versão pública que use um token compartilhado precisaria de um servidor para guardá-lo. Inserir um token próprio no JavaScript público permitiria que qualquer visitante o copiasse.

## Organização dos arquivos

| Arquivo | Papel |
| --- | --- |
| index.html | Estrutura das três telas, formulários, diálogos e créditos. |
| style.css | Paleta, tipografia, layouts responsivos, estados e movimento reduzido. |
| theme-cinema.css | Nova identidade escura, composição de projeção e adaptações visuais. |
| script.js | Busca, validação, estado da coleção, renderização, eventos e animações. |
| assets/hero-projection.png | Arte original da projeção, preservada como fonte visual. |
| assets/hero-projection-dark.png | Versão horizontal escura aplicada à abertura. |
| assets/brand-system-dark.png | Quadro da nova identidade visual do projeto. |
| assets/fonts/ | Fontes locais usadas na interface. |
| design-philosophy.md | Ideia visual que orientou a identidade e o layout. |

## Como os dados circulam

```text
Coleção de demonstração ou resposta do TMDb
                 ↓
       normalização do filme
                 ↓
      cartões da aba Descobrir
                 ↓ adicionar / editar
  coleção pessoal em memória + localStorage
                 ↓
   Minha lista, resumo e Meu painel
```

A API devolve campos como poster_path e genre_ids. normalizeTmdbFilm() converte esses dados para o formato usado pelo app: id, title, year, genres, overview e poster. Assim, catálogo e dados de demonstração passam pelos mesmos componentes.

## Pontos para estudar

- **loadLibrary()** valida o JSON persistido antes de criar os registros. Isso evita confiar em dados inválidos guardados no navegador.
- **renderAll()** redesenha os resumos e as telas a partir de library; os cartões refletem o estado e não o substituem.
- **cardFor() e posterFor()** criam elementos com document.createElement() e inserem conteúdo com textContent, sem interpretar títulos e notas como HTML.
- **Delegação de eventos** mantém os cliques funcionando mesmo quando os cartões são recriados.
- **AbortController** interrompe buscas antigas para que uma resposta atrasada não substitua uma consulta mais recente.
- **renderStats()** calcula nota e gêneros só com os registros correspondentes; as anotações são ordenadas pela atualização mais recente.
- **initMotion() e revealCards()** isolam os efeitos do GSAP. A interface mantém seu estado visual padrão quando a biblioteca não carrega ou quando a pessoa prefere menos movimento.

## Créditos do TMDb

O catálogo opcional e seus cartazes vêm do TMDb. O rodapé mantém o logo e a declaração obrigatória: “This product uses the TMDB API but is not endorsed or certified by TMDB.” Veja o [FAQ oficial do TMDb](https://developer.themoviedb.org/docs/faq). A API é gratuita para uso não comercial com atribuição e está sujeita aos termos do TMDb.
