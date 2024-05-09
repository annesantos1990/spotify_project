<h1 align="center"> <a href="https://open.spotify.com/user/exll9wa5yql2llqyi1k5h56qm?si=YkkYuaD7SN60DMjXWo7eTQ&utm_source=copy-link" target="_blank"> <img src="https://github.com/mrankitgupta/Spotify-Data-Analysis-using-Python/blob/main/images/social-spotify.svg" alt="Spotify" width="55" height="40"/> </a> Spotify Data Analysis   </h1>

<sub>**Avaliação das músicas mais ouvidas no Spotify em 2023**<sub>



Time responsável pelo projeto:
Maiully Mendoça e Eslaine Santos

### Caso

Em um mercado altamente competitivo, uma gravadora precisa inserir um novo artista no cenário global da música. Assim, essa gravadora viu a necessidade de tomar decisões estratégicas baseadas em dados.

A gravadora levantou uma série de hipóteses sobre o que faz uma música seja mais ouvida. Essas hipóteses incluem:

- Músicas com BPM (Batidas Por Minuto) mais altos fazem mais sucesso em termos de número de streams no Spotify.
- As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas, como a Deezer.
- A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams.
- Artistas com um maior número de músicas no Spotify têm mais streams.
- As características da música influenciam o sucesso em termos de número de streams no Spotify.

 <h2>Objetivo</h2> 

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

<details> <summary> <h3> Limpeza dos Dados </h3>  - Clique em ▶ para ver os detalhes </summary> 
    
→ As etapas de limpeza de dados desse projeto foram feitas no Big Query. 

→ Nome do projeto criado pelo time no Big Query: **hipoteses-proj2**

#### Valores nulos

Primeiro, fizemos a contabilização dos valores nulos. Com esse propósito, usamos a seguinte consulta no *Big Query*:

```sql
SELECT COUNT(*) AS numNulls
  FROM `hipoteses-proj2.dados_proj2.joined_table`
  WHERE variável x IS NULL
```

Assim, conseguimos fazer a contabilização dos valores nulos das variáveis das três tabelas.

Após as consultas foram encontradas as seguintes contagens para os valores nulos:

- Tabela **Competition**
    - Lista de variáveis com valores Nulos:
     **in_shazam_charts:** 50 -
        - Não foi eliminada. Os valores nulos foram substituídos pela moda dessa variável. O valor da moda foi escolhido por conta da variabilidade alta dos dados.
        - Foi escolhido substituir os valores nulos da variável  **in_*shazam_*charts** pela moda dos valores dessa variável:

```sql
  SELECT 
    *,
    COALESCE(in_shazam_charts, moda_coluna) AS in_shazam_charts_moda
  FROM 
    `hipoteses-proj2.dados_proj2.track_in_competition`,
    (SELECT in_shazam_charts AS moda_coluna
     FROM `hipoteses-proj2.dados_proj2.track_in_competition`
     GROUP BY in_shazam_charts
     ORDER BY COUNT(in_shazam_charts) DESC
     LIMIT 1) AS moda_subquery
),
```    
- Tabela **Spotify**
    - Lista de variáveis com valores Nulos: Não foi encontrada variáveis que tivesse valores nulos.

- Tabela **Technical_info**
    **key:** 95 -  
        A variável **key** foi eliminada, pois não foi preciso avaliar essa variável.


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

### Valores Discrepantes

Para limpeza dos carateres especiais da variável do tipo STRING, foi feita a seguinte consulta:

```sql
SELECT
UPPER(REPLACE(track_id, ':', '')) AS track_id,
UPPER(REPLACE(track_name, '�', '')) AS track_name,
UPPER(REPLACE(artist_s__name, '�', '')) AS artist_s__name,
artist_count,
DATE(released_year,released_month,released_day) AS release_date,
in_spotify_playlists,
in_spotify_charts,
streams
FROM `hipoteses-proj2.dados_proj2.track_in_spotify`
```

Para a limpeza das variáveis numéricas, foi usada a seguinte consulta:

```sql
SELECT
  CAST(variável AS INT64) stream_INT
FROM (
  SELECT
    streams
  FROM
    `tabela
  WHERE
    SAFE_CAST(variável AS INT64) IS NOT NULL)

```

Através desse script, eliminamos o dado no formato STRING e convertemos a coluna toda para o formato INTEGER:

Onde, 

SAFE_CAST(variável AS INT64): Retorna nulo, caso o dado da variável não seja um INTEGER válido;

WHERE  SAFE_CAST(variável AS INT64) IS NOT NULL - Retorna todos os valores não nulos da conversão feita através do SAFE_CAST;

CAST(variável AS INT64) novo_nome_coluna - Converte as variáveis que não deram valor nulo na subquery.

Consulta no Big Query para identificar esses valores discrepantes, eliminação e conversão desses dados :

[joined_table](https://docs.google.com/document/d/1ZNy_2ubbzKyfwMVetiIF_uhLJb4SKlAqyufjmuzeX0U/edit?usp=sharing)

### Valores outliers

→ Outliers são pontos de dados que estão significativamente distantes do restante dos dados em uma distribuição. Eles podem ser valores muito altos ou muito baixos em relação à média ou mediana da distribuição.

→ Foi analisado os valores outliers por meio de gráficos de dispersão:

- **track_in_competition**
    
    ![Captura de Tela 2024-04-14 às 22.01.24.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/2708b09c-85d8-4650-83fe-5bc45d403f8f/b03da617-068c-407c-97a6-a7ec970aacd6.png)
    
    ![Captura de Tela 2024-04-14 às 22.07.09.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/aea251fb-9c6a-4941-a6e7-cb78b5df82c7/e8952267-6b43-46d4-89b0-5f6f34286659.png)
    
    ![Captura de Tela 2024-04-14 às 22.10.21.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/9a874b67-79d7-41aa-b87a-ff342059ac7a/15de899e-3fa2-496c-a5b1-b10b22e18dc1.png)
    
    ![Captura de Tela 2024-04-14 às 22.15.11.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/97b7125a-f0ae-474e-8c5d-e52bbc436b7e/c1814a40-8f7c-438b-b38c-f31ff49ae8fd.png)
    
- **track_in_spotify**
    
    ![Captura de Tela 2024-04-15 às 08.52.21.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/8e99e5c0-74df-4531-bc62-f4b7adc214c8/c76dbfa9-76ed-4cb0-b1f0-bdcd14f8aa6f.png)
    
    ![Captura de Tela 2024-04-15 às 08.52.58.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/bfa36a2e-b08b-4967-88a4-12eb58000060/9c5d937d-dcdc-421d-ad8d-592285ebfd4a.png)
    
    ![Captura de Tela 2024-04-15 às 08.53.28.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/4bbf00d9-bd09-414b-85e3-c96343f7becf/ae07969e-8676-4d66-b0b4-f8963f89e2ff.png)
    
    ![Captura de Tela 2024-04-15 às 08.53.49.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/7517d47e-ea0a-4a9c-a629-e4d9a5b29b19/2d61260b-02d9-49f4-989e-9ee1e759e86b.png)
    
    ![Captura de Tela 2024-04-15 às 08.54.16.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/035fd572-9a9a-46d7-84ee-4e5ead189351/dd6e86c9-143d-46a8-a0d0-5d0899b6a096.png)
    
    ![Captura de Tela 2024-04-15 às 08.54.38.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/70ae6d45-10a8-4a97-8fc5-48e8ee53b3a6/46681d54-db47-4723-b7d5-5778ba23377d.png)
    
    ![Captura de Tela 2024-04-15 às 08.55.00.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/4c1e67b0-0da2-4ec7-a554-4de22fa63849/510dc172-6c22-4c75-9e26-4c561aa75108.png)
    
- **track_technical_info**
    
    ![Captura de Tela 2024-04-14 às 20.17.59.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/66e884f9-c11d-4d26-a6d1-7299bf216a61/Captura_de_Tela_2024-04-14_as_20.17.59.png)
    
    ![Captura de Tela 2024-04-14 às 20.19.21.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/aee25629-aa18-4b32-94f2-f297844158b8/Captura_de_Tela_2024-04-14_as_20.19.21.png)
    

Analisando os gráficos acima, vimos que os valores das variáveis são bastante heterogêneos, com vários outliers, optamos em não excluir esses outliers, porque para a análise do cenário musical, é importante entender o comportamento desses outliers, que representam na maioria das variáveis, os artistas que possuem um maior destaque nesse cenário.

### **Novas variáveis**

Foram criadas duas novas variáveis:

Data de lançamento: Fizemos através do comando DATE

```sql
DATE(released_year,released_month,released_day) AS release_date,
```

Total de Playlist. Que simplesmente é a soma de determinada música em todas as playlists:

```sql
spotify_clean.in_spotify_playlists + competition_clean.in_deezer_playlists + competition_clean.in_deezer_playlists AS total_playlists,
```

### Código Completo e união das tabelas

Combinamos todos os códigos apresentados na sessões anteriores em uma única consulta, que uniu as três tabelas como mostrado abaixo:

```sql
-- tabela unificada

WITH 
spotify_clean AS (
  SELECT
    UPPER(REPLACE(track_id, ':', '')) AS track_id,
    UPPER(REPLACE(track_name, '�', '')) AS track_name,
    UPPER(REPLACE(artist_s__name, '�', '')) AS artist_s__name,
    artist_count,
    DATE(released_year,released_month,released_day) AS release_date,
    in_spotify_playlists,
    in_spotify_charts,
    streams
  FROM `hipoteses-proj2.dados_proj2.track_in_spotify`
  QUALIFY streams IS NOT NULL
    AND ROW_NUMBER() OVER(PARTITION BY track_name, artist_s__name ORDER BY track_name, artist_s__name) = 1
),
competition_clean AS (
  SELECT 
    *,
    COALESCE(in_shazam_charts, moda_coluna) AS in_shazam_charts_moda
  FROM 
    `hipoteses-proj2.dados_proj2.track_in_competition`,
    (SELECT in_shazam_charts AS moda_coluna
     FROM `hipoteses-proj2.dados_proj2.track_in_competition`
     GROUP BY in_shazam_charts
     ORDER BY COUNT(in_shazam_charts) DESC
     LIMIT 1) AS moda_subquery
),
technical_info AS (
  SELECT 
  * EXCEPT (key)
  FROM `hipoteses-proj2.dados_proj2.track_technical_info`
),
conversao_stream AS (
  SELECT 
  *,
  CAST(streams AS INT64) stream -- Faz a conversão para INTEGER
  FROM (
    SELECT
      *
    FROM
      `hipoteses-proj2.dados_proj2.track_in_spotify`
    WHERE
      SAFE_CAST(streams AS INT64) IS NOT NULL)
) 

SELECT 
  spotify_clean.track_id,
  spotify_clean.track_name,
  spotify_clean.artist_s__name,
  spotify_clean.artist_count,
  spotify_clean.release_date,
  spotify_clean.in_spotify_playlists,
  spotify_clean.in_spotify_charts,
  competition_clean.in_apple_playlists,
  competition_clean.in_apple_charts,
  competition_clean.in_deezer_playlists,
  competition_clean.in_deezer_charts,
  competition_clean.in_shazam_charts_moda,
  spotify_clean.in_spotify_playlists + competition_clean.in_deezer_playlists + competition_clean.in_deezer_playlists AS total_playlists,
  conversao_stream.stream ,
  technical_info.bpm,
  technical_info.danceability__,
  technical_info.valence__,
  technical_info.energy__,
  technical_info.acousticness__,
  technical_info.instrumentalness__,
  technical_info.liveness__,
  technical_info.speechiness__,
  technical_info.mode
FROM competition_clean
JOIN spotify_clean ON competition_clean.track_id = spotify_clean.track_id
JOIN technical_info ON competition_clean.track_id = technical_info.track_id
JOIN conversao_stream ON competition_clean.track_id = conversao_stream.track_id 
ORDER BY spotify_clean.artist_s__name;
```

Nesse código, foi listada as variáveis que iria sem inclusas na tabela final através do SELECT e optamos em não adicionar a variável Key, pois ela não ajudaria a responder a nenhuma das perguntas e hipóteses iniciais desse projeto

### Tabelas Auxiliar

Fizemos uma tabela auxiliar com o propósito de fazer uma consulta do total de músicas de artistas solo:

```
WITH 
solo_songs AS (
  SELECT 
    artist_s__name,
    COUNT(*) AS total_solo_songs,
    AVG(stream) AS avg_streams
  FROM `hipoteses-proj2.dados_proj2.joined_table` 
  WHERE artist_count = 1
  GROUP BY artist_s__name
)

SELECT 
  DISTINCT solo_songs.artist_s__name,
  solo_songs.total_solo_songs,
  solo_songs.avg_streams
FROM `hipoteses-proj2.dados_proj2.joined_table` artist_name
JOIN solo_songs ON artist_name.artist_s__name = solo_songs.artist_s__name;
```


</details>

<details> <summary> <h3> Análise Exploratória dos Dados</h3>  - Clique em ▶ para ver os detalhes </summary> 

#### Medidas de Tendência Central


Os detalhes da análise exploratória, poderá ser visto na Seção **Resultados e Discussão**.
</details>

### Metodologia


### Resultados e Discussão

### Conclusões

### Recomendações

### Limitações




