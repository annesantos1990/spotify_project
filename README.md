<h1 align="center"> <a href="https://open.spotify.com/user/exll9wa5yql2llqyi1k5h56qm?si=YkkYuaD7SN60DMjXWo7eTQ&utm_source=copy-link" target="_blank"> <img src="https://github.com/mrankitgupta/Spotify-Data-Analysis-using-Python/blob/main/images/social-spotify.svg" alt="Spotify" width="55" height="40"/> </a> Spotify Data Analysis   </h1>

<sub>**Avaliação das músicas mais ouvidas no Spotify em 2023**<sub>



Equipe responsável pelo projeto:
Maiully Mendoça e Eslaine Santos

### Caso

Em um mercado altamente competitivo, uma gravadora precisa inserir um novo artista no cenário global da música. Assim, essa gravadora viu a necessidade de tomar decisões estratégicas baseadas em dados.

A gravadora levantou uma série de hipóteses sobre o que faz uma música seja mais ouvida. Essas hipóteses incluem:

- Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de número de streams no Spotify.
- As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas, como a Deezer.
- A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams.
- Artistas com um maior número de músicas no Spotify têm mais streams.
- As características da música influenciam o sucesso em termos de número de streams no Spotify.

### Objetivo

- O objetivo dessa análise é ajudar a gravadora e o artista a tomar decisões baseadas nos dados que aumentem suas chances de ter sucesso nesse mercado

- Objetivo do analista
    
    Você deve validar (refutar ou confirmar) as hipóteses levantadas através da análise de dados e fornecer recomendações estratégicas com base em suas descobertas. O objetivo principal desta análise é que a gravadora e o novo artista possam tomar decisões informadas que aumentem suas chances de alcançar o “sucesso”.

### Ferramentas
- BigQuery (linguagem SQL): para gerenciamento de dados.
- Power BI: para visualização de dados.
- Google Colab (Python): para realizar análises em Python.

### Biblioteca de Dados

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

<details>
<summary>  ### Limpeza dos Dados <summary>
    
#### **Processar e preparar base de dados**

As etapas de limpeza de dados desse projeto foram feitas no Big Query. 

Nome do projeto criado pela dupla no Big Query: **hipoteses-proj2**

As consultas foram salvas posteriomente no Google Docs, por conta da limitação de 90 dias de armazenamento das consultas na versão gratuita.

#### Valores nulos

Primeiro, fizemos a contabilização dos valores nulos. Com esse propósito, usamos a seguinte consulta no *Big Query*:

```sql
SELECT
  COUNT(*)
FROM `tabela X
WHERE variável is null

```

Ex.:

```sql
SELECT COUNT(*) AS numNulls
  FROM `hipoteses-proj2.dados_proj2.joined_table`
  WHERE mode IS NULL
```

Assim, conseguimos fazer a contabilização dos valores nulos das variáveis das três tabelas.

Link da consulta feita no *Big Query* - Salva no Google Docs:  

[check_joined_table](https://docs.google.com/document/d/1ZOSlBYejAB1MROC7VJ9Xj5lEGrBBtqwThFz6sqb6qf4/edit?usp=sharing)

Após as consultas foram encontradas as seguintes contagens para os valores nulos:

- Tabela **Competition**
    - Lista de variáveis:
    
    | Variável | Contagem de valores Nulos | Eliminar dados com valores nulos? |
    | --- | --- | --- |
    | track_id | 0 |  |
    | in_apple_playlists | 0 |  |
    | in_apple_charts | 0 |  |
    | in_deezer_playlists | 0 |  |
    | in_deezer_charts | 0 |  |
    | in_shazam_charts | 50 | Nao eliminamos. Escolhemos substituir os valores nulos pela moda dessa variável. O valor da moda foi escolhido por conta da variabilidade alta dos dados. |
    

- Tabela **Spotify**
    - Lista de variáveis:
    
    | Variável | Contagem de valores Nulos | Eliminar dados com valores nulos? |
    | --- | --- | --- |
    | track_id | 0 |  |
    | track_name | 0 |  |
    | artist(s)_name | 0 |  |
    | artist_count | 0 |  |
    | released_year | 0 |  |
    | released_month | 0 |  |
    | released_day | 0 |  |
    | in_spotify_playlists | 0 |  |
    | in_spotify_charts | 0 |  |
    | streams | 0 |  |

- Tabela **Technical_info**
    
    
    | Variável | Contagem de valores Nulos | Eliminar dados com valores nulos? |
    | --- | --- | --- |
    | track_id | 0 |  |
    | bpm | 0 |  |
    | key | 95 |  |
    | mode | 0 |  |
    | danceability_% | 0 |  |
    | valence_% | 0 |  |
    | energy_% | 0 |  |
    | acusticness_% | 0 |  |
    | instrumentality_% | 0 |  |
    | liveness_% | 0 |  |
    | speechiness_% | 0 |  |

Foi escolhido substituir os valores nulos da variável  **in_*shazam_*charts** pela média dos valores dessa variável:

```sql
 /*consulta para substituir os nulos (NULL) pela média dos valores da variável*/
SELECT
  *,
  IFNULL(in_shazam_charts, (
    SELECT
      AVG(in_shazam_charts)
    FROM
      `projeto-2-laboratoria.Spotify.Competition`)) AS in_shazam_charts_corrg
FROM
  `projeto-2-laboratoria.Spotify.Competition` 
```

No caso da variável **key**, optamos por não adicionar na tabela unida, pois não foi preciso avaliar essa variável.

#### Valores duplicados

Para a identificação dos valores duplicados, utilizamos a seguinte consulta no *Big Query*:

```sql
-- Código usado para contar o número de células duplicadas:
SELECT track_id, COUNT(track_id)
  FROM `hipoteses-proj2.dados_proj2.joined_table`
  GROUP BY track_id
  HAVING COUNT(track_id) > 1;

-- Código para verificar linhas em que track_name, artist_s__name se repetem:
SELECT track_name, artist_s__name, COUNT(*) as count
    FROM `hipoteses-proj2.dados_proj2.joined_table`
    GROUP BY track_name, artist_s__name
    HAVING count > 1
```

Link da consulta feita:

[check_joined_table](https://docs.google.com/document/d/1ZOSlBYejAB1MROC7VJ9Xj5lEGrBBtqwThFz6sqb6qf4/edit?usp=sharing)

Para cada tabela, analisamos os valores duplicados apenas das variáveis relevantes. A seguir, detalhamos qual variável foi examinada e por que optamos por investigar os duplicados dessa variável:

Tabela **Competition**

| Variável | Valores duplicados | Razão |
| --- | --- | --- |
| track_id | 0 | Essa variável reapresenta um identificador exclusivo de cada música. Se houver valores duplicados, isso indica a presença de músicas repetidas no banco de dados. |

Tabela **Spotify**

| Variável | Valores duplicados | Razão |
| --- | --- | --- |
| track_name e artist_s__name | 4 | Foi escolhido identificar os valores duplicados simultaneamente dessas duas variáveis, pois pode haver mais de um uma música do mesmo artista e mais de uma música com mesmo nome com artistas diferentes. |

Tabela **Techical_info**

| Variável | Valores duplicados | Razão |
| --- | --- | --- |
| track_id | 0 | Essa variável reapresenta um identificador exclusivo de cada música. Se tiver valores duplicados, significa que tem músicas repetidas no banco de dados |
|  |  |  |

**Dados que estão duplicados na tabela Spotify:**

| Música | Artista | Qt duplicada |
| --- | --- | --- |
| SNAP | Rosa Linn | 2 |
| About Damn Time | Lizzo | 2 |
| Take My Breath | The Weeknd | 2 |
| SPIT IN MY FACE! | ThxSoMch | 2 |

Para eliminar os valores duplicados, usamos a seguinte Query: 

```sql
/*Consulta para retirar os dados duplicados permanentemente da tabela original*/
CREATE OR REPLACE TABLE
  `projeto-2-laboratoria.Spotify.spotify` AS
SELECT *
FROM `projeto-2-laboratoria.Spotify.spotify`
QUALIFY ROW_NUMBER() OVER(PARTITION BY track_name, artist_s__name ORDER BY track_name, artist_s__name) = 1;
```

Essa Query, eliminou somente as repetições.

No qual, QUANTIFY representa um filtro que vai retorna toda vez que o ROW NUMBER( ) = 1 

Foi usado esse comando QUANTIFY como filtro por conta do PARTITION BY.
</details>

#### Novas Variáveis

### Resultados e Discussão

### Conclusões

### Recomendações

### Limitações




