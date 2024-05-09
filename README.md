# Avaliação das músicas mais ouvidas no Spotify em 2023


Esse projeto foi feito em parceria com Mayully Mendonça: 

## Caso

Em um mercado altamente competitivo, uma gravadora precisa inserir um novo artista no cenário global da música. Assim, essa gravadora viu a necessidade de tomar decisões estratégicas baseadas em dados.

A gravadora levantou uma série de hipóteses sobre o que faz uma música seja mais ouvida. Essas hipóteses incluem:

- Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de número de streams no Spotify.
- As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas, como a Deezer.
- A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams.
- Artistas com um maior número de músicas no Spotify têm mais streams.
- As características da música influenciam o sucesso em termos de número de streams no Spotify.

- ## Objetivo

- O objetivo dessa análise é ajudar a gravadora e o artista a tomar decisões baseadas nos dados que aumentem suas chances de ter sucesso nesse mercado

- Objetivo do analista
    
    Você deve validar (refutar ou confirmar) as hipóteses levantadas através da análise de dados e fornecer recomendações estratégicas com base em suas descobertas. O objetivo principal desta análise é que a gravadora e o novo artista possam tomar decisões informadas que aumentem suas chances de alcançar o “sucesso”.

  ## - BigQuery (linguagem SQL): para gerenciamento de dados.
- Power BI: para visualização de dados.
- Google Colab (Python): para realizar análises em Python.

- ## Biblioteca de Dados

- **Que dados temos?**

Para esse projeto, tivemos a disposição três diferentes tabelas: Competition, Spotify e Technical_info. Abaixo tem as tabelas e as descrições das variáveis de cada uma delas.

- Tabela **Competition**
    - Lista de variáveis:
    
    | Variável | Descrição |
    | --- | --- |
    | track_id | Identificador exclusivo da música. É um número inteiro de 7 dígitos que não se repete. |
    | in_apple_playlists | número de listas de reprodução da Apple Music em que a música está incluída. |
    | in_apple_charts | Presença e classificação da música nas paradas da Apple Music. |
    | in_deezer_playlists | Número de playlists do Deezer em que a música está incluída. |
    | in_deezer_charts | Presença e posição da música nas paradas da Deezer. |
    | in_shazam_charts | Presença e classificação da música nas paradas da Shazam. |
- Tabela **Spotify**
    - Lista de variáveis:
    
    | Variável | Descrição |
    | --- | --- |
    | track_id | Identificador exclusivo da música. É um número inteiro de 7 dígitos que não se repete. |
    | track_name | Nome da música. |
    | artist(s)_name | Nome do(s) artista(s) da música. |
    | artist_count | Número de artistas que contribuíram na música. |
    | released_year | Ano em que a música foi lançada. |
    | released_month | Mês em que a música foi lançada. |
    | released_day | Dia do mês em que a música foi lançada. |
    | in_spotify_playlists | Número de listas de reprodução do Spotify em que a música está incluída |
    | in_spotify_charts | Presença e posição da música nas paradas do Spotify |
    | streams | Número total de streams no Spotify. Representa o número de vezes que a música foi ouvida. |
- Tabela **Technical_info**
    
    
    | Variável | Descrição |
    | --- | --- |
    | track_id | Identificador exclusivo da música. É um número inteiro de 7 dígitos que não se repete. |
    | bpm | Batidas por minuto, uma medida do tempo da música. |
    | key | Tom musical da música. |
    | mode | Modo de música (maior ou menor). |
    | danceability_% | Porcentagem que indica o quão apropriado a canção é para dançar |
    | valence_% | Positividade do conteúdo musical da música. |
    | energy_% | Nível de energia percebido da música. |
    | acusticness_% | Quantidade de som acústico na música. |
    | instrumentality_% | Quantidade de conteúdo instrumental na música. |
    | liveness_% | Presença de elementos de performance ao vivo. |
    | speechiness_% | Quantidade de palavras faladas na música. |

  ## Limpeza dos Dados

  ## Novas Variáveis

  ## Resultados e Discussão

  ## Conclusão

  ## Recomendações

  ## Limitações
