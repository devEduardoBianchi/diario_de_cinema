# Entre Cenas

**Seu diário de cinema.** Descubra filmes, organize sua próxima sessão e registre o que ficou depois dela.

Aplicação web responsiva feita com HTML, CSS e JavaScript puro. Ela abre com um catálogo de demonstração e não precisa de conta, instalação de dependências ou etapa de compilação.

## O que você pode fazer

- Explorar filmes de demonstração ou buscar títulos no catálogo do TMDb.
- Montar uma lista pessoal, marcar filmes como vistos e editar ou remover registros.
- Guardar uma nota, a data em que assistiu e uma anotação sobre cada filme.
- Filtrar e ordenar a coleção, acompanhar estatísticas e percorrer as anotações recentes.
- Usar a interface em desktop ou celular, com navegação por teclado e suporte a movimento reduzido.

## Executar localmente

Para executar localmente de forma estável, use Python 3. No terminal, dentro desta pasta, inicie um servidor:

```powershell
py -3 -m http.server 8000 --bind 127.0.0.1
```

Depois, abra <http://127.0.0.1:8000/>. No macOS ou Linux, o comando costuma ser `python3 -m http.server 8000 --bind 127.0.0.1`.

O catálogo e os recursos locais funcionam sem configuração adicional. As capas de demonstração são carregadas do TMDb e precisam de conexão à internet.

## Busca opcional pelo TMDb

Para buscar no catálogo completo, crie sua própria conta no [TMDb](https://www.themoviedb.org/), obtenha um **API Read Access Token** nas configurações e informe-o em **Configurar catálogo** dentro do app. Sem token, o catálogo de demonstração continua disponível.

O token informado é mantido em `sessionStorage` nesta aba e enviado diretamente ao TMDb no cabeçalho da busca. Ele não está incluído no código do repositório. Trate-o como uma credencial pessoal: não o cole em arquivos do projeto nem em commits. A coleção, as avaliações e as anotações ficam em `localStorage` neste navegador; o app não tem conta, sincronização ou servidor próprio.

As capas e a busca usam serviços do TMDb. O app mantém no rodapé a atribuição: “This product uses the TMDB API but is not endorsed or certified by TMDB.” Consulte o [FAQ oficial do TMDb](https://developer.themoviedb.org/docs/faq) para conhecer os requisitos de uso e atribuição.

## Tecnologias e identidade

- HTML semântico, CSS responsivo e JavaScript sem framework.
- GSAP 3.15.0 e ScrollTrigger para revelar conteúdo e dar movimento à abertura. Se a biblioteca não carregar, os recursos do app continuam disponíveis.
- Fraunces nos títulos e Space Grotesk nos textos, servidas localmente. Os arquivos de licença SIL Open Font License estão em `assets/fonts/`.
- Tema **Sala de projeção**: carvão, marfim e âmbar, com arte original e animações que respeitam `prefers-reduced-motion`.

## Organização

| Arquivo | Conteúdo |
| --- | --- |
| `index.html` | Estrutura da página, diálogos, formulários e créditos. |
| `style.css` | Estilos base, componentes e layouts responsivos. |
| `theme-cinema.css` | Tema escuro, composição cinematográfica e fontes. |
| `script.js` | Catálogo, coleção local, busca, filtros, estatísticas e animações. |
| `assets/` | Arte do projeto e fontes com suas licenças. |
| `design-philosophy.md` | Ideia visual por trás da identidade e da composição. |

## Licença

O código do aplicativo ainda não tem uma licença declarada. Tornar o repositório público não concede automaticamente permissão para reutilizar ou redistribuir o código. As fontes incluídas mantêm as licenças próprias em `assets/fonts/`.
