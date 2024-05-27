<h1 align="center"> <a href="https://open.spotify.com/user/exll9wa5yql2llqyi1k5h56qm?si=YkkYuaD7SN60DMjXWo7eTQ&utm_source=copy-link" target="_blank"> <img src="https://github.com/mrankitgupta/Spotify-Data-Analysis-using-Python/blob/main/images/social-spotify.svg" alt="Spotify" width="55" height="40"/> </a> Spotify Data Analysis <img src="https://github.com/annesantos1990/spotify_project/assets/166059836/79e9bc2c-1feb-485e-bcf8-8e1b38e7a1f3" alt="Spotify" width="120" height="45"/>  </h1>

<sub>**Avaliação das músicas mais ouvidas no Spotify em 2023 feita para a gravadora Mix Master**<sub>

**Time responsável pelo projeto**: Maiully Mendoça e Eslaine Santos
##

<p align="center">
 
[Caso](#caso)  •  [Principais Hipóteses](#principais-hipóteses)  •  [Objetivo](#objetivo)  •  [Ferramentas](#ferramentas)   •  [Resultados e Discussão](#resultados-e-discussão)  •  [Conclusões](#conclusões)  •  [Recomendações](#recomendações)  •  [Venha nos conhecer!](#venha-nos-conhecer)

</p>


## Caso

Em um mercado altamente competitivo, a gravadora Mix Master precisa inserir um novo artista no cenário global da música. Assim, essa gravadora viu a necessidade de tomar decisões estratégicas baseadas em dados.

## Principais Hipóteses

- Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de número de streams no Spotify.
- As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas, como a Deezer.
- A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams.
- Artistas com um maior número de músicas no Spotify têm mais streams.
- As características da música influenciam o sucesso em termos de número de streams no Spotify.

 <h2>Objetivo</h2> 

- O objetivo dessa análise é ajudar a gravadora e o artista a tomar decisões baseadas nos dados que aumentem suas chances de ter sucesso nesse mercado

  - Objetivo do analista
      
      Validar (refutar ou confirmar) as hipóteses levantadas através da análise de dados e fornecer recomendações estratégicas com base em suas descobertas.


## Ferramentas
- BigQuery (linguagem SQL): para gerenciamento de dados.
- Power BI: para visualização de dados.
- Google Colab (Python): para realizar análises em Python.


### Biblioteca e Tratamento do Dados

O tratamento e parte das análises dos dados foi feita no *Big Query*.
Para mais detalhes da biblioteca e do tratamento do dados, basta clicar nesse link: [Clique aqui](https://github.com/annesantos1990/limpezadedados_spotify)

### Visualização dos dados - PowerBi
Parte dos gráficos que estão apresentados na seção de resultados foi feito no PowerBi. Para acessar o dashboard feito nessa ferramenta, clique no Link abaixo:
[Clique aqui ou na imagem](https://app.powerbi.com/view?r=eyJrIjoiZmU2ZTdjZTktYWQyOS00YjcwLTgyNDUtODM3ZmRhMDdiMTQ5IiwidCI6ImUwZjY3ODE5LTJmNmYtNDg0Mi1hZjVlLTA5ZjI4Y2U4N2U0NyJ9&pageName=ReportSection566586d215a102c1dbbe)

[![Texto Alternativo](https://github.com/annesantos1990/spotify_project/assets/166059836/908e0d4c-dbea-4b4e-8078-6dce037f9265)](https://app.powerbi.com/view?r=eyJrIjoiZmU2ZTdjZTktYWQyOS00YjcwLTgyNDUtODM3ZmRhMDdiMTQ5IiwidCI6ImUwZjY3ODE5LTJmNmYtNDg0Mi1hZjVlLTA5ZjI4Y2U4N2U0NyJ9&pageName=ReportSection566586d215a102c1dbbe)



### Análise dos dados - Google Colab
Para a análise dos dados desse projeto foi utilizado o Google Colab. Para visulizar os códigos utilizados para as análises que serão vista na seção de resultados, acesse o Notebook: [Clique aqui](https://github.com/annesantos1990/spotify_project/blob/bc8bbc84bc77dcbff635e6db280220ea13a2feba/proj2_colaborativo.ipynb           )

## Apresentação do projeto
Para ver os slides com a apresentação do projeto [clique aqui.](https://github.com/annesantos1990/spotify_project/blob/main/Projeto%20Spotify.pdf)
 
## Resultados e Discussão
A análise detalhada desse projeto com os gráficos e discussões pode ser vista em nossa página pública do Notion: [Clique aqui](https://crystal-haumea-eb9.notion.site/Resultados-e-Conclus-es-dfc2af5e8eef4460ae8428b746c82511?pvs=4)


Mas aqui, vou fazer um resumo dos principais resultados encontrados:

**Análise Geral:**

→ Das músicas mais ouvidas em 2023, a maioria foi lançada após 2019, sugerindo uma preferência por músicas mais recentes.

→ Houve um aumento significativo nos streams de músicas lançadas após 2017 em comparação com aquelas lançadas anteriormente.

→ As músicas lançadas recentemente são divulgadas extensivamente nas redes sociais e plataformas online, o que pode aumentar seu tempo nas listas de tendências e sua popularidade. 

**Top 10 Artistas e Músicas:**

→ Taylor Swift lidera tanto em número de músicas quanto em streams.

→ 6 das 10 músicas mais ouvidas são colaborações entre artistas.

**Streams por Mês de Lançamento:**

→ Músicas lançadas em janeiro e em maio se destacam.

→ O que pode estar associado a estratégias de lançamento para coincidir com eventos sazonais, como antecipação dos festivais de verão em países nórdicos e uma maior abertura a novidades no mês de janeiro.


**Hipóteses:**

   **Correlação Forte:**

 Músicas presentes em muitas playlists têm mais streams:
  - O que parece natural, já que o esperado é que as músicas que são colocadas em mais playlists sejam mais vistas
  - Isso reforça a importância de estratégias que visem aumentar a inclusão de músicas em playlists podem potencializar seu desempenho em termos de streams. Isso pode envolver campanhas de divulgação direcionadas a curadores de playlists (4).
Artistas com mais músicas no Spotify tendem a acumular mais streams:
  -  Fortalece a ideia de que os artistas que buscam aumentar sua audiência e obter mais sucesso na carreira musical devem realizar lançamentos frequentes de músicas.

**Correlação Moderada:**

As músicas mais populares no ranking do Spotify  possui uma correlação moderada com o ranking em outras plataformas como Deezer:

- Diversos fatores podem influenciar a popularidade de uma música em cada plataforma, incluindo preferências de público-alvo, estratégias de marketing, algoritmos de recomendação e promoção específica em cada plataforma. Portanto, enquanto pode haver uma tendência geral de que músicas populares em uma plataforma também tenham uma presença significativa em outras, essa relação não é determinística e varia dependendo de diversos contextos e condições específicas de cada plataforma e do comportamento do público.

**Correlação Fraca:**
As características da música não influenciam o sucesso em termos de streams no Spotify:

- Isso indica que, embora esses elementos sejam importantes para o estilo e identidade musical de um artista, a popularidade das músicas não parece ser determinada exclusivamente por suas características musicais, e outros fatores podem estar desempenhando um papel mais significativo na determinação do sucesso das faixas.
   


## Conclusões
A partir das análises realizadas, identificamos os principais fatores que parecem influenciar a popularidade das músicas no Spotify:

- Quantidade de músicas que um artista lança;
    - A quantidade de músicas lançadas por um artista e sua presença em playlists emergiram como elementos cruciais associados à popularidade das faixas.
- Estar em uma maior parte das playlists aumenta a probabilidade de alcançar um público mais amplo e, consequentemente, mais streams.

Por outro lado, observamos que alguns fatores não demonstraram ser tão determinantes para a popularidade das músicas no Spotify:

- As características individuais das músicas, não apresentaram uma correlação significativa com a quantidade de streams. Isso indica que, embora esses elementos possam contribuir para o estilo e identidade musical de uma faixa, eles não são os principais impulsionadores de sua popularidade em plataformas de streaming.
- A época do ano não foi diretamente relacionada à popularidade das músicas. Isso sugere que outros fatores, além do calendário sazonal, desempenham um papel mais significativo na determinação do sucesso das faixas.

## Recomendações
Desenvolver uma Estratégia de Lançamento: Planejar e executar lançamentos regulares de músicas, mantendo uma presença consistente no mercado musical.

• Networking com Curadores de Playlists: Entrar em contato com curadores de playlists relevantes e promover ativamente suas músicas para inclusão em playlists populares.

• Diversificar a Presença em Plataformas: Além do Spotify, considerar a promoção e distribuição da música em outras plataformas de streaming para alcançar um público mais amplo.

• Considerar a diversificação da presença em outras plataformas de streaming além do Spotify, aproveitando a associação moderada entre as diferentes plataformas para expandir o alcance do público.

• Enfatizar a qualidade e autenticidade das músicas, em vez de se concentrar em características específicas que não demonstraram ter um impacto direto na popularidade.

• Explorar oportunidades de colaboração e parceria com outros artistas de forma equilibrada, evitando sobrecarregar as faixas com um número excessivo de colaboradores.

## Limitações
Muitos fatores podem influenciar o número de streams, e muitos deles são externos ao Spotify, o que não é possível avaliar devido aos dados serem quase que exclusivamente provenientes dessa plataforma, com apenas algumas outras variáveis provenientes de plataformas de menor destaque como Deezer, Apple e Shazam.

Por isso, investigar a influência de fatores externos é importante. Como exemplo, podemos considerar o impacto de ouvir um clipe no YouTube ou em outras redes sociais na quantidade de vezes que uma música será reproduzida no Spotify.

Além disso, restringir os dados apenas às músicas mais ouvidas em um único ano pode limitar a generalização dos resultados, pois não considera a diversidade e a evolução do cenário musical ao longo do tempo

### Links das referências:
(1) https://newsroom.spotify.com/company-info/
(2) https://newsroom.spotify.com/2023-05-24/crossover-collaborations-genre-collabs-streaming-data-spotify/
(3) https://blog.symphonic.com/2024/01/11/best-and-worst-months-to-release-music/
(4) [https://newmusicbrasil.blog/2022/09/16/saiba-o-que-e-e-o-porque-a-playlist-de-curadoria-e-tao-importante/#:~:text=Um curador é o responsável,sentido estar dentro da playlist](https://newmusicbrasil.blog/2022/09/16/saiba-o-que-e-e-o-porque-a-playlist-de-curadoria-e-tao-importante/#:~:text=Um%20curador%20%C3%A9%20o%20respons%C3%A1vel,sentido%20estar%20dentro%20da%20playlist).

## Venha nos conhecer!

Quer saber mais sobre as autoras desse projeto? Acesse o nosso LinkedIn:

https://www.linkedin.com/in/maiully-data-analyst/

https://www.linkedin.com/in/eslaine-santos-e-santos-46159a28/

Obrigada por sua atenção!




