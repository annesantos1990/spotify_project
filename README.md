<h1 align="center"> <a href="https://open.spotify.com/user/exll9wa5yql2llqyi1k5h56qm?si=YkkYuaD7SN60DMjXWo7eTQ&utm_source=copy-link" target="_blank"> <img src="https://github.com/mrankitgupta/Spotify-Data-Analysis-using-Python/blob/main/images/social-spotify.svg" alt="Spotify" width="55" height="40"/> </a> Spotify Data Analysis   </h1>

<sub>**Avaliação das músicas mais ouvidas no Spotify em 2023**<sub>



**Time responsável pelo projeto**: Maiully Mendoça e Eslaine Santos





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


### Biblioteca e Tratamento do Dados

O tratamento e parte das análises dos dados foi feita no *Big Query*.
Para mais detalhes da biblioteca e do tratamento do dados, basta clicar nesse link: [Clique aqui](https://github.com/annesantos1990/limpezadedados_spotify)

### Visualização dos dados - PowerBi
Parte dos gráficos que estão apresentados na seção de resultados foi feito no PowerBi. Para acessar o dashboard feito nessa ferramenta, clique no Link abaixo:
https://app.powerbi.com/view?r=eyJrIjoiZmU2ZTdjZTktYWQyOS00YjcwLTgyNDUtODM3ZmRhMDdiMTQ5IiwidCI6ImUwZjY3ODE5LTJmNmYtNDg0Mi1hZjVlLTA5ZjI4Y2U4N2U0NyJ9

[![Texto Alternativo](https://github.com/annesantos1990/spotify_project/assets/166059836/908e0d4c-dbea-4b4e-8078-6dce037f9265)](https://app.powerbi.com/view?r=eyJrIjoiZmU2ZTdjZTktYWQyOS00YjcwLTgyNDUtODM3ZmRhMDdiMTQ5IiwidCI6ImUwZjY3ODE5LTJmNmYtNDg0Mi1hZjVlLTA5ZjI4Y2U4N2U0NyJ9)


![3](https://github.com/annesantos1990/spotify_project/assets/166059836/908e0d4c-dbea-4b4e-8078-6dce037f9265)

### Análise dos dados - Google Colab
Para a análise dos dados desse projeto foi utilizado o Google Colab. Para visulizar os códigos utilizados para as análises que serão vista na seção de resultados, acesse o Notebook: [Clique aqui](https://github.com/annesantos1990/spotify_project/blob/bc8bbc84bc77dcbff635e6db280220ea13a2feba/proj2_colaborativo.ipynb           )


 
## Resultados e Discussão
### Análise Exploratória


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

![1](https://github.com/annesantos1990/spotify_project/assets/166059836/36a46366-b986-484e-8742-e6151768c88a)

→ O gráfico abaixo mostra a quantidade de streams por ano de lançamento da música:

![2](https://github.com/annesantos1990/spotify_project/assets/166059836/fda3dbe7-a452-4879-98c1-ea2cff5d8685)

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




