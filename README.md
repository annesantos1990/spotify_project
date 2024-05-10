<h1 align="center"> <a href="https://open.spotify.com/user/exll9wa5yql2llqyi1k5h56qm?si=YkkYuaD7SN60DMjXWo7eTQ&utm_source=copy-link" target="_blank"> <img src="https://github.com/mrankitgupta/Spotify-Data-Analysis-using-Python/blob/main/images/social-spotify.svg" alt="Spotify" width="55" height="40"/> </a> Spotify Data Analysis   </h1>

<sub>**Avaliação das músicas mais ouvidas no Spotify em 2023**<sub>



**Time responsável pelo projeto**: Maiully Mendoça e Eslaine Santos

**Notebook do Google Colab** com os códigos utilizados para as análises: [Clique aqui]( https://colab.research.google.com/drive/119geWP5ptsqI5TKIUUcVjuHzDP8Ym9tK#scrollTo=W51ocgiq-h8Q)

https://github.com/annesantos1990/spotify_project/blob/bc8bbc84bc77dcbff635e6db280220ea13a2feba/proj2_colaborativo.ipynb

proj2_colaborativo.ipynb

## Caso

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


## Ferramentas
- BigQuery (linguagem SQL): para gerenciamento de dados.
- Power BI: para visualização de dados.
- Google Colab (Python): para realizar análises em Python.

## Biblioteca de Dados

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

<details> <summary> <h2> Limpeza dos Dados </h2>  - Clique em ▶ para ver os detalhes </summary> 
    
→ As etapas de limpeza de dados desse projeto foram feitas no Big Query. 

→ Nome do projeto criado pelo time no Big Query: **hipoteses-proj2**

### Valores nulos

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


### Valores duplicados

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
<details> <summary> <h2> Análise Exploratória dos Dados</h2>  - Clique em ▶ para ver os detalhes </summary> 

### Medidas de Tendência Central


Os detalhes da análise exploratória, poderá ser visto na Seção **Resultados e Discussão**.
</details>

## Resultados e Discussão
### Análise Exploratória

---

<aside>
🎼 Ano de lançamento do Spotify: 2008

</aside>

### Análise de streams por data de lançamento das músicas

→ Os dados para essa análise, se tratam das músicas mais ouvidas no ano de 2023. Ao analisar o ano de lançamento das músicas desse banco de dados, é possível observar:

- Músicas com lançamentos antes de 2019: 184
- Músicas com lançamentos depois de 2019: 763

Obs.: É importante ressaltar que os dados utilizados para esta análise constituem uma amostra, o que pode potencialmente limitar algumas conclusões. Atualmente, a plataforma do Spotify abriga um acervo de mais de 100 milhões de faixas [(1)](https://www.notion.so/37e342c0ae0f49e8b45b9378ecb685f4?pvs=21).

→ Quanto as músicas mais ouvidas em 2023, segregadas por ano de lançamento e com base em nossa amostragem: 

- Antes de 2019: 201 bilhões de streams
- Depois de 2019: 286 bilhões de streams

→ Quando comparamos os streams por ano de lançamento antes e depois de 2017, a diferença é ainda maior.

- Antes de 2017: Aproximadamente 157 bilhões
- Depois de 2017: Aproximadamente 329 bilhões

→ O gráfico abaixo mostra o total de músicas por ano de lançamento

![Captura de tela 2024-05-08 175801.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/33971dce-2ea5-4f75-b05c-b54ce8f7ec5e/Captura_de_tela_2024-05-08_175801.png)

→ O gráfico abaixo mostra a quantidade de streams por ano de lançamento da música:

![Captura de tela 2024-05-08 110401.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/db7b24af-6ca2-4392-8488-b955031bd2b4/99321a7c-c089-4570-9e42-ea3640b8b3f7.png)

→ Observa-se que as pessoas tendem a ouvir mais músicas lançadas recentemente, algumas possíveis explicações são:

- As músicas lançadas atualmente são divulgadas extensivamente em diversas plataformas sociais, o que as mantém por mais tempo nas listas de tendências. Isso pode contribuir significativamente para o aumento do número de streams de faixas lançadas recentemente.
- Também é interessante pensar que atualmente os artistas divulgam os seus lançamentos nas redes sociais e em plataformas da internet, isso pode influenciar para que as músicas lançadas recentemente sejam mais populares.
- A quantidade de músicas que foram lançadas a partir de 2017 é consideravelmente maior do que a quantidade de músicas que foram lançadas em anos anteriores.

**Para resumir essa análise, vamos listar os dez artistas com mais streams, os dez com mais lançamentos e as dez músicas com mais strems:**

| Top 10 artistas com mais músicas | Top 10 artistas com mais streams | 10 músicas com mais streams |
|---------|---------|---------|
|1. Taylor Swift | 1. Taylor Swift  | 1. Taylor Swift |
|2. The Weekend  | 2. The Weekend  | 2. Ed Sheeran |
|3. Bad Bunny | 3. Bad Bunny | 3. The Weekend |
|4. Sza | 4. Sza | 4. Harry Styles |
|5. Harry Styles | 5. Harry Styles | 5. Bad Bunny |
|6. Kendrick Lamar | 6. Kendrick Lamar | 6. Oliva Rodrigo |
|7. Morgan Wallen | 7. Morgan Wallen | 7. Eminem |
|8. Ed Sheeran | 8. Ed Sheeran | 8. Bruno Mars |
|9. BTS | 9. BTS | 9. Arctic Monkeys |
|10. Drake, 21 Savage | 10. Drake, 21 Savage | 10. Imagine Dragons|

 

![Captura de tela 2024-05-08 111739.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/d4c8f2e2-82e4-4fbb-9fd0-47e97df7259a/Captura_de_tela_2024-05-08_111739.png)

 ![Captura de tela 2024-05-08 111615.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/12ade75f-577d-4681-8c37-b8ce3a9ac4c8/Captura_de_tela_2024-05-08_111615.png)

![Captura de tela 2024-05-08 112037.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/914fe2a0-1f77-4530-8471-b0eec52f5cce/Captura_de_tela_2024-05-08_112037.png)

→ Cinco dos artistas mais ouvidos, cujo volume de streams é significativo, coincidem com aqueles que têm a maior quantidade de músicas mais ouvidas. Essa observação sugere que os artistas mais populares têm uma presença significativa no top das músicas mais ouvidas. Isso indica que os artistas mais ouvidos tendem a ter um grande número de faixas que se destacam nas listas de tendências. Essa associação entre o sucesso dos artistas e a popularidade de suas músicas pode refletir a capacidade desses artistas de criar conteúdo musical que ressoa com o público e mantém sua relevância nas plataformas de streaming.

→ Adicionalmente, é interessante notar que seis das músicas presentes no top 10 das mais ouvidas são duetos. Isso pode sugerir que colaborações entre artistas, especialmente em formato de duetos, têm potencial para atrair uma audiência significativa e alcançar posições de destaque nas listas de reprodução. Esse fenômeno pode ser atribuído à combinação de diferentes estilos musicais e à curiosidade dos ouvintes em relação à interação entre os artistas envolvidos [(2)](https://www.notion.so/Refer-ncias-1-4a4744e08a9f40fdb6948d8c93f3dcce?pvs=21).

### Streams por mês de lançamento das músicas

A proposta desta análise é investigar qual é o mês de lançamento das músicas mais ouvidas para identificar algum padrão de preferência ou sazonalidade entre os ouvintes.

Para isso, elaboramos os gráficos a seguir, que representa a série temporal dos streams das músicas lançadas mensalmente ao longo dos anos, juntamente com um gráfico de barras que mostra, entre as músicas mais ouvidas, em qual mês de lançamento houve mais destaque. 

![Captura de tela 2024-05-08 181040.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/150a8f07-b42c-46d1-b3da-346df6368b71/Captura_de_tela_2024-05-08_181040.png)

É possível observar que, entre as músicas lançadas antes de 2018, aquelas lançadas em janeiro estão mais em destaque. Por outro lado, após 2018, notamos que as músicas lançadas em maio se destacam mais. Essa tendência pode ser atribuída a uma série de fatores, como estratégias de lançamento por parte dos artistas e gravadoras, pois o mês de janeiro, é dito como o melhor mês de lançamento, porque as pessoas estão ansiosas por novidade e não estão tão saturadas como no final do ano e os ouvintes estão mais abertos a coisas novas. E por conta dos festivais de verão (a maioria dos países de língua inglesa se encontram no norte), o mês de maio é um bom mês, pois é um mês que precede a esses festivais (3).

### Segmentação
---

**📌  Os testes estatísticos realizados ao segmentar a variável "stream" em categorias de alto e baixo, com base nas características das músicas, produziram os seguintes resultados:**

|  | Teste  | Estatística do Teste (U)  | P-valor | Diferença Significativa |
| --- | --- | --- | --- | --- |
| 0 |  Danceability  | 91423.000000   | 0.038764                      | Sim |
| 1 |  Valence  | 1.450275   | 0.147314                      | Não |
| 2 | Energy               | 0.658124   | 0.510619                      | Não |
| 3 | Acousticness               | 0.349773   | 0.726587                      | Não |
| 4 | Instrumentalness               | 1.794559   | 0.073044                      | Não |
| 5 | Liveness               | 0.707211   | 0.479610 | Não |
|  | Speechiness           | 93234.000000   | 0.010345                      | Sim |

→ Os testes realizados revelaram diferenças estatisticamente significativas para as variáveis Danceability e Speechiness ao segmentar os grupos de stream em categorias de alto e baixo, conforme indicado pelos valores baixos do p-valor.

→ No teste de Mann-Whitney, a estatística de teste U é calculada para avaliar se há diferença entre os grupos. Um p-valor menor que 0,05 sugere que a diferença observada não é devida ao acaso e permite rejeitar a hipótese nula. No caso presente, os p-valores foram inferiores a 0,05 para as variáveis Danceability e Speechiness, indicando diferenças estatisticamente significativas entre os grupos.

→ No entanto, é importante destacar que o p-valor não fornece informações sobre a magnitude da diferença entre os grupos, apenas se essa diferença é improvável de ocorrer ao acaso. 

**📌 Gráfico Boxplot dos grupos testados:**

![box plot.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/ac0718c5-675d-4b60-9f2a-0b8a0c65acef/box_plot.png)

**📌 Modo da música e a quantidade de streams:**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/0a4df76a-a96d-4c13-af26-59e5b65e36c3/Untitled.png)

- O gráfico revela que os valores de streams para cada modo estão bem distribuídos em ambos os grupos. Isso sugere que o modo da música parece não exercer influência significativa sobre a quantidade de streams.

### Hipóteses

#### **Hipótese 1: Músicas com BPM (Beats Per Minute) mais altos fazem mais sucesso em termos de streams no Spotify.**

| Variável Independente | Variável Independente | Correlação | Nível da correlação |
| --- | --- | --- | --- |
| BPM | Streams |  -0.0023061 | Baixa |

![gráfico de dispersão.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/a058779f-afc8-47c0-8bed-a7e2d7886033/0b0dfa97-b23d-4b39-a180-60e921d40b5d.png)

→ A Hipótese 1 sugere que músicas com um maior número de BPM (Beats Per Minute) tendem a ser mais bem-sucedidas em termos de streams no Spotify. No entanto, não foi identificada uma correlação forte entre essas variáveis.

→ Isso significa que, após análises estatísticas, não foi encontrada uma associação significativa ou consistente entre o número de BPM de uma música e o seu sucesso em termos de streams no Spotify. Em outras palavras, a velocidade da música, medida em BPM, não parece ter uma influência decisiva na quantidade de streams que ela recebe na plataforma.

#### **Hipótese 2: As músicas mais populares no ranking do Spotify também possuem um comportamento semelhante em outras plataformas como Deezer.**

| Variável Independente | Variável Dependente | Correlação | Nível da correlação |
| --- | --- | --- | --- |
| In_spotify_charts | In_deezer_charts |  0.599986   | Moderada |
| In_spotify_charts | In_apple_charts | 0.551428   | Moderada |
| In_spotify_charts | In_shazam_charts | 0.571838     | Moderada |

![gráfico de dispersão.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/04e94d42-28e3-4a80-b03c-71f32dec6975/5a2e6593-5f1a-4940-b753-9cfb663de9e2.png)

→ A Hipótese 2 propõe que as músicas mais populares no ranking do Spotify também apresentam um desempenho semelhante em outras plataformas, como o Deezer. Foi identificada uma correlação moderada entre todas as variáveis testadas: in_spotify_charts vs. in_deezer_charts, in_spotify_charts vs. in_apple_charts e in_spotify_charts vs. in_shazam_charts.

→ Isso significa que há uma associação moderada entre a presença de uma música nos rankings do Spotify e sua presença nos rankings do Deezer, Apple Music e Shazam. Em outras palavras, as músicas que são populares no Spotify tendem a ter uma presença semelhante em termos de popularidade nessas outras plataformas, mas essa associação não é tão forte a ponto de ser considerada altamente correlacionada.

→ Em termos reais, não é possível afirmar categoricamente que uma música que esteja classificada em uma posição alta em um determinado ranking em uma plataforma estará necessariamente bem classificada em outro ranking em outra plataforma. Embora tenha sido identificada uma correlação moderada entre as variáveis testadas, isso indica apenas uma associação estatística entre a presença das músicas nos rankings das diferentes plataformas, não uma relação de causa e efeito.

→ Diversos fatores podem influenciar a popularidade de uma música em cada plataforma, incluindo preferências de público-alvo, estratégias de marketing, algoritmos de recomendação e promoção específica em cada plataforma. Portanto, enquanto pode haver uma tendência geral de que músicas populares em uma plataforma também tenham uma presença significativa em outras, essa relação não é determinística e varia dependendo de diversos contextos e condições específicas de cada plataforma e do comportamento do público.

### **Hipótese 3: A presença de uma música em um maior número de playlists está relacionada com um maior número de streams.**

**Dentre as 236 músicas com alto número de streams, sabemos que:**

→ São músicas com alto número de playlists no Spotify: 196

→ São músicas com alto número de playlists na Apple: 158

→ São músicas com alto número de playlists no Deezer: 182

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/8a6fdd7e-9cfb-4443-8abc-0ca274e5f534/4bfae1b9-121f-4063-9055-99f60691cd96.png)

A análise feita acima mostra que músicas presentes em muitas playlists tendem a ter um número maior de streams. Isso é plausível, uma vez que a inclusão frequente de uma música em várias playlists aumenta sua exposição aos usuários, o que pode resultar em um aumento na sua reprodução.
A Hipótese 3 sugere que a presença de uma música em um maior número de playlists está relacionada com um maior número de streams. Com esse propósito, calculamos a correlação do total de playlists que uma música está inserida em relação ao quanto ela é ouvida (quantidade de streams):

| Variável Dependente | Variável Independente | Correlação | Nível da correlação |
| --- | --- | --- | --- |
| total_playlist | stream |  0.771199 | Alta |

![gráfico de dispersão.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/b6b72d54-24df-45bf-8844-59363f66f0bf/efd0c764-19a7-4391-ae97-5d2802b2ce34.png)

A análise revelou uma correlação significativa entre as variáveis total_playlist e o total de streams. Como já foi mencionado, esse achado é coerente, uma vez que a frequente inclusão de uma música em diversas playlists expande sua visibilidade junto aos usuários. Ao figurar em um número maior de playlists, uma música se depara com mais oportunidades de ser descoberta e ouvida por um público mais amplo, o que, por sua vez, pode culminar em um notável aumento no número de streams.

Portanto,  a correlação observada entre a quantidade de playlists e o número de streams reforça a ideia de que estratégias que visem aumentar a inclusão de músicas em playlists podem potencializar seu desempenho em termos de streams. Isso pode envolver campanhas de divulgação direcionadas a curadores de playlists [(4)](https://www.notion.so/Refer-ncias-1-f94127250dea4be999fa02fba2ad4763?pvs=21), colaborações com outros artistas ou influenciadores, promoção cruzada entre plataformas de streaming e a criação de conteúdo envolvente para incentivar a inclusão da música em playlists por parte dos usuários.

### **Hipótese 4: Artistas com maior número de músicas no Spotify têm mais streams.**

| Variável Independente | Variável Dependente | Correlação | Nível da correlação |
| --- | --- | --- | --- |
| total_playlist | stream | 0.778368 | Alta |

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/55765bf9-7c8e-4ab6-802a-03fc78b4f3cc/b7757685-a0ad-415e-9a52-7ce231d9da4a.png)

A hipótese 2 sugere que artistas com um maior número de músicas no Spotify acumulam mais streams. Como evidenciado pelo gráfico e pela correlação entre essas variáveis, os artistas que lançam mais músicas tendem a ser mais ouvidos. No início da análise dos resultados, foi observado que cinco dos artistas mais ouvidos também estavam no top 10 de artistas com mais lançamentos.

Essa constatação, juntamente com a análise da correlação entre essas duas variáveis, fortalece a ideia de que os artistas que buscam aumentar sua audiência e obter mais sucesso na carreira musical devem realizar lançamentos frequentes de músicas.

### **Hipótese 5: As características da música influenciam o sucesso em termos de streams no Spotify.**

A hipótese 5 sugere que as características da música exercem influência sobre o sucesso em termos de streams no Spotify. De forma geral, constatamos que não há uma correlação significativa entre as características das músicas e sua popularidade, como pode ser observado na tabela abaixo:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/2ef4a216-4c14-4b17-91b1-0897e09e5074/914f527a-2a17-4f95-b584-15a19ace191b.png)

As músicas dos artistas mais ouvidos apresentam uma diversidade considerável em suas características, não permitindo a identificação de um padrão claro.

Essa conclusão é reforçada pela análise da correlação entre as características das músicas e sua popularidade, medida pela quantidade de streams, como evidenciado nos gráficos de dispersão abaixo e suas respectivas correlações:

| Variável Independente | Variável Dependente | Correlação | Nível da correlação |
| --- | --- | --- | --- |
| Energia | Stream | -0,02607719892 | Baixa |
| Instrumentailidade | Stream | -0,04411944418 | Baixa |
| Valência | Stream | -0,04084334972 | Baixa |
| Speechiness | Stream | -0.112367113835 | Baixa |
| Dançabilidade | Stream | -0,1055557718 | Baixa |
| Acústica | Stream | -0,004701274453 | Baixa |
| Vivência | Stream | -0,04995471886 | Baixa |

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/49b68f03-6e9b-4d63-8665-185baae8660d/b89e91dd-e893-421a-b00c-1ecbb546da8d.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/7cabf1e5-aa63-4af3-981d-858816b6876d/fab8cf0d-472e-45ec-81e9-ea10cf11572d.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/3737cd68-bf10-42eb-9bcf-48a3e13b67c8/b11d6627-7b3b-4511-a3bd-d061b7b3bf60.png)

Para os artistas mais ouvidos, observa-se que algumas correlações apresentam variações. Por exemplo, no caso de Taylor Swift, há um aumento na correlação das variáveis dançabilidade e valência com a quantidade de streams. Similarmente, para Ed Sheeran, é observado um aumento na correlação das variáveis dançabilidade, valência e acústica com o número de streams.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/ba2a75f8-5167-4c9c-af29-e60feef98c46/6b8541bd-b0dc-42c9-89f0-9e274cd0b2dc.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/96ce458e-4cd7-45d8-82df-d2448e99f353/b2989707-6ba9-4c99-9acb-f025454081ee.png)

Porém, percebe-se que não há um padrão consistente em relação à correlação dessas variáveis, pois para o 3º e o 4º artistas mais ouvidos, não se observa esse mesmo comportamento.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/25822403-0202-4f4a-85a4-d9975c48c73a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/c66eb433-de53-4554-8280-86efd7e804b7/Untitled.png)

Em resumo, não ter encontrado uma correlação significativa para a Hipótese 5 indica que não há uma relação estatisticamente relevante entre as características das músicas e sua popularidade em termos de streams no Spotify. Isso sugere que, dentro da amostra analisada, características como dançabilidade, energia, instrumentalidade, acústica e valência das músicas não têm um impacto direto ou consistente na quantidade de streams que recebem. 

Isso indica que, embora esses elementos sejam importantes para o estilo e identidade musical de um artista, a popularidade das músicas não parece ser determinada exclusivamente por suas características musicais, e outros fatores podem estar desempenhando um papel mais significativo na determinação do sucesso das faixas.

### **Hipóteses adicionais: Música com mais artistas envolvidos na faixa, possuem maior quantidade de stream.**

Testamos uma nova hipótese: se músicas com mais artistas envolvidos na faixa apresentariam mais streams. Com esse propósito, calculamos a correlação (R-pearson) entre as variáveis **Artista por música**, obtida através da consulta feita no Big Query, e a variável Stream. O valor de R-pearson e o gráfico de dispersão com sua respectiva regressão indicam uma correlação muito baixa entre essas variáveis:

| Variável Independente | Variável Dependente | Correlação | Nível da correlação |
| --- | --- | --- | --- |
| Artista por música | stream | -0.13632 | Baixa |

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/43eb7214-874e-4104-bde8-123b7f57e545/dd78213d-e6e2-44b6-9b29-733407847a82/Untitled.png)

Entretanto, ao analisar o gráfico acima, é possível observar que as músicas com poucos artistas envolvidos na faixa apresentam uma variabilidade considerável. Isso sugere que, para esse grupo (1 a 3 artistas por música), existem faixas com tanto baixo quanto alto número de streams. Por outro lado, no grupo de músicas com 4 artistas por música ou mais, a quantidade de streams tende a ser mais uniformemente baixa.

Essa observação nos leva a concluir que, por algum motivo, canções com muitos artistas por música tendem a não atrair muitos streams. Isso pode ser atribuído a uma série de fatores, como a complexidade da colaboração entre múltiplos artistas, a diluição da identidade musical da faixa ou até mesmo a falta de promoção adequada.

### Conclusões
A partir das análises realizadas, identificamos os principais fatores que parecem influenciar a popularidade das músicas no Spotify:

- Quantidade de músicas que um artista lança;
    - A quantidade de músicas lançadas por um artista e sua presença em playlists emergiram como elementos cruciais associados à popularidade das faixas.
- Estar em uma maior parte das playlists aumenta a probabilidade de alcançar um público mais amplo e, consequentemente, mais streams.

Por outro lado, observamos que alguns fatores não demonstraram ser tão determinantes para a popularidade das músicas no Spotify:

- As características individuais das músicas, não apresentaram uma correlação significativa com a quantidade de streams. Isso indica que, embora esses elementos possam contribuir para o estilo e identidade musical de uma faixa, eles não são os principais impulsionadores de sua popularidade em plataformas de streaming.
- A época do ano não foi diretamente relacionada à popularidade das músicas. Isso sugere que outros fatores, além do calendário sazonal, desempenham um papel mais significativo na determinação do sucesso das faixas.

### Recomendações
Desenvolver uma Estratégia de Lançamento: Planejar e executar lançamentos regulares de músicas, mantendo uma presença consistente no mercado musical.

• Networking com Curadores de Playlists: Entrar em contato com curadores de playlists relevantes e promover ativamente suas músicas para inclusão em playlists populares.

• Diversificar a Presença em Plataformas: Além do Spotify, considerar a promoção e distribuição da música em outras plataformas de streaming para alcançar um público mais amplo.

• Considerar a diversificação da presença em outras plataformas de streaming além do Spotify, aproveitando a associação moderada entre as diferentes plataformas para expandir o alcance do público.

• Enfatizar a qualidade e autenticidade das músicas, em vez de se concentrar em características específicas que não demonstraram ter um impacto direto na popularidade.

• Explorar oportunidades de colaboração e parceria com outros artistas de forma equilibrada, evitando sobrecarregar as faixas com um número excessivo de colaboradores.

### Limitações
Muitos fatores podem influenciar o número de streams, e muitos deles são externos ao Spotify, o que não é possível avaliar devido aos dados serem quase que exclusivamente provenientes dessa plataforma, com apenas algumas outras variáveis provenientes de plataformas de menor destaque como Deezer, Apple e Shazam.

Por isso, investigar a influência de fatores externos é importante. Como exemplo, podemos considerar o impacto de ouvir um clipe no YouTube ou em outras redes sociais na quantidade de vezes que uma música será reproduzida no Spotify.

### Links das referências:
(1) https://newsroom.spotify.com/company-info/
(2) https://newsroom.spotify.com/2023-05-24/crossover-collaborations-genre-collabs-streaming-data-spotify/
(3) https://blog.symphonic.com/2024/01/11/best-and-worst-months-to-release-music/
(4) [https://newmusicbrasil.blog/2022/09/16/saiba-o-que-e-e-o-porque-a-playlist-de-curadoria-e-tao-importante/#:~:text=Um curador é o responsável,sentido estar dentro da playlist](https://newmusicbrasil.blog/2022/09/16/saiba-o-que-e-e-o-porque-a-playlist-de-curadoria-e-tao-importante/#:~:text=Um%20curador%20%C3%A9%20o%20respons%C3%A1vel,sentido%20estar%20dentro%20da%20playlist).




