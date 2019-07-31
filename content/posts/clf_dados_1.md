<<<<<<< HEAD
+++
title = "dados: como classificá-los?"
date = 2019-07-29T15:07:26-03:00
draft = false
thumbnail = "images/dados_clf_01.png"
+++

=======
---
title: "dados: como classificá-los?"
date: 2019-07-29T15:07:26-03:00
draft: false
images:
- /images/clf_dados_1/dados_clf_01.png
---
>>>>>>> 2e562342919b913d515056e8757847a4cc4a074c


A grande maioria dos [**mapas temáticos**](https://en.wikipedia.org/wiki/Thematic_map) faz uso de algum método para [**classificação de dados**](http://www.gitta.info/Statistics/en/html/StandClass_learningObject2.html). O objetivo desse processo é organizar os dados em intervalos de dados ou em classes. A classificação se torna necessária para evitar um nível de granularidade muito elevado tornando a informação incompreensiva. Por outro lado, como apresentado em *[**How to lie with maps**](https://www.ft.com/content/65b5df0e-49ff-11e8-8ee8-cae73aab7ccb)* um agrupamento incorreto pode distorcer a informação. Atualmente, existem programas ([QGIS](https://www.qgis.org/pt_BR/site/), [ArcGIS](https://www.arcgis.com/index.html), [GeoPandas](http://geopandas.org/), etc.) que automatizam a produção de mapas com várias configurações *default* para "facilitar" a vida do usuário. Todavia, tais facilidades podem esconder armadilhas para usuários menos experientes.

>Dados podem ser facilmente <span style="color:#AC4142"><b>distorcidos</b></span> quando analistas sucumbem ao senso de seguir as sugestões padrão das soluções de software. Por exemplo, a maior parte das vezes que um software gera um [mapa coroplético](https://pt.wikipedia.org/wiki/Mapa_coropl%C3%A9tico) a classificação utilizada nos dados é realizada por uma segmentação em 5 categorias baseada em intervalos iguais ou por quantis. (Livre Tradução) <i>Lying with Maps</i>, Mark Monmonier, Statistical Science, 2005, Vol. 20, No. 3, 215–222

<center><img src="https://media.giphy.com/media/McsujjSqA3a7ogIxHb/giphy.gif" width="55%" height="50%" /></center>

Em termos técnicos, o objetivo da classificação de dados é distribuir um conjunto de dados em N categorias, de modo a minimizar <strong>a variância dentro dos grupos e maximizá-la entre os grupos</strong>. Por exemplo, considere o conjunto de dados a seguir, que representa leituras fictícias de [pH](https://pt.wikipedia.org/wiki/PH).

<center><img src="/images/clf_dados_1/array.png"/></center>

Iniciamos o processo com a determinação do <span style="color:#AC4142">**número de classes**</span> (**N**) e com a escolha do <span style="color:#AC4142">**método**</span> de categorização. A definição de **N** está associado a pergunta: **O quanto de generalização você deseja em seus dados?** Quanto maior for **N** menor será a generalização associada aos dados, todavia, muitas classes poderão implicar em problemas de legibilidade. Dessa forma, o recomendado é algo em torno de 3 a 7 classes. De sorte que, como regra de ouro, um bom início é avaliar o uso de **5 classes**. Quanto ao **método** iremos utilizar o de **[intervalo iguais](http://wiki.gis.com/wiki/index.php/Equal_Interval_classification).** Assim**,** calculamos a amplitude (**A**), para pH temos uma escala adimensional entre 0 e 14, portanto, **A = 14**. Para calcular o intervalo intra classe: **A/N=2.8**. Assim, concluímos a definição da distribuição dos dados em diferentes intervalos.

<center><img src="/images/clf_dados_1/escala_ph_equal_interval.png"  width="30%" height="30%"/></center>

Uma das características desse método é a criação de classes com tamanho iguais. Todavia, quase sempre haverá uma distribuição desbalanceada dos dados nas diferentes categorias, podendo ocorrer alguma distorção por [viés amostral](https://pt.wikipedia.org/wiki/Erro_amostral) em alguma classe, por exemplo. Por outro lado, a decisão de como realizar essa estratificação dos dados <span style="color:#AC4142"><strong>pode</strong></span> levar em conta o <span style="color:#AC4142"><strong>contexto</strong></span> da análise. O pH é uma medida utilizada em diversas áreas profissionais para mensurar o quão alcalino ou ácido um determinado meio é, como bem apresenta a ilustração abaixo do [Guia do Estudante](https://www.notion.so/netoferraz/CLASSIFICADORES-DE-DADOS-0ace9ee9022b4915b22bb03e838135c5#ac4421462c2b4abe803572bf84e08d9c).

<center><img src="/images/clf_dados_1/escala_pH.png" width="50%" height="50%"/></center>

Vamos imaginar que você trabalhe em um órgão ambiental estadual que deve controlar o pH da água do mar das praias de uma cidade. É sabido que a [água do mar é levemente alcalina](https://www.portaleducacao.com.br/conteudo/artigos/biologia/potencial-hidrogenionico-ph-da-agua-do-mar/33752), com pH entre 7,4 a 8,5. Além disso, vamos supor que a série histórica apresente uma média de 7.5 ± 1.2. Uma categorização pode ser efetuada usando-se uma medida de tendência central em conjunto com uma medida de dispersão, como a média e o desvio-padrão (DP), respectivamente. Dessa forma, criamos intervalos contextualizados aos dados. De modo que seja possível avaliar se as leituras de pH estão coerentes com o <span style="color:#AC4142"><strong>target</strong></span>, isto é, a média da série histórica.

<center><img src="/images/clf_dados_1/pH_DP_example.png" width="40%" height="40%"/></center>


A escolha do método de classificação influenciará o trabalho do analista. Ao ponto que histórias distintas podem ser contadas a partir de um mesmo conjunto de dados. Por exemplo, na figura abaixo são mostradas as escalas de cores produzidas por dois métodos distintos. Assim, são nítidas as mudanças de classificação. Portanto, histórias diferentes podem ser contadas a partir dessas escolhas.

<center><img src="/images/clf_dados_1/tipos_de_classificacao_comparacao_corrigido.png"/></center>

Havendo uma compreensão inicial do que são métodos de classificação de dados e o seu objetivo, podemos explorar com maiores detalhes as principais abordagens existentes. Dessa forma, é válido ressaltar que não há uma única maneira de determinar um número de classes ideal e tampouco um melhor método. Assim, o caminho mais seguro é <span style="color:#AC4142"><strong>conhecer</strong></span> os prós e contras de cada abordagem e verificar se ela é apropriada ao seu conjunto de dados em particular.

<center><img src="https://media.giphy.com/media/9MIJgbU0YOhQjddI92/giphy.gif" width="55%" height="50%" /></center>

Achou que iria ser <span style="color:#AC4142"><strong>molezinha</strong></span>? Eu também! Mas vamos lá, que não é tão complicado quanto pode parecer. Nesse post, vamos detalhar 4 dos classificadores mais utilizados:

1. Intervalos iguais (<i>Equal Interval</i>)
2. Quebras naturais (<i>Natural Breaks</i>)
3. Quantis (<i>Quantiles</i>)
4. Customizado (<i>User Defined</i>)

A  <span style="color:#AC4142"><strong>Análise Exploratória de Dados (AED)</strong></span>, disseminada pelo cientista [John Tukey](https://pt.wikipedia.org/wiki/John_Tukey), permanece importante nos dias atuais. Várias das técnicas propostas, a serem realizadas durante o processo de <span style="color:#AC4142"><strong>AED</strong></span>, nos auxiliarão na tomada de decisão de qual método de classificação é mais apropriado para os seus dados. Para uma melhor compreensão do tópico, convoquei dois personagens que irão me auxiliar a melhor apresentar o assunto. São eles: <strong>Seu Creysson</strong> e <strong>Bino</strong>. Os dois atuarão como facilitadores de aprendizagem, em que o <strong>Seu Creysson</strong> sempre fará os apontamentos que são considerados <u>corretos</u>, enquanto o <strong>Bino</strong> se encarregará de indicar onde estão as <u>ciladas</u>.

<center><img src="/images/clf_dados_1/facilitadores_de_aprendizagem2.png"/></center>

### 1. Intervalos iguais (<i>Equal interval</i>)

Como mencionado, serão nossos aliados a <span style="color:#AC4142"><strong>AED</strong></span>, a compreensão da distribuição dos dados - por meio de histogramas e de outras visualizações - e o entedimento do assunto estudado.

<center><img src="/images/clf_dados_1/EAD_data_structure.PNG"/></center>

O método de <span style="color:#AC4142"><strong>intervalos iguais</strong></span> realiza uma divisão em classes com intervalos de mesmo tamanho, sendo mais apropriado a dados que se distribuam de forma semelhante por toda a amplitude do dataset. A seguir, temos como exemplo a categorização de um conjunto de dados arbitrário, que possui uma amplitude 100 unidades. Efetuamos a divisão do conjunto em 5 classes, com 20 unidades associadas a cada classe.

<center><img src="/images/clf_dados_1/equal_interval_example.png"/></center>

O conhecimento sobre as mais diversas [distribuições de probabilidade](https://pt.wikipedia.org/wiki/Distribui%C3%A7%C3%A3o_de_probabilidade) será um aliado importante na tomada de decisão de como classificar os dados. O método de intervalos iguais se apresenta como uma boa opção para dados que se apresentem como uma [distribuição uniforme](https://pt.wikipedia.org/wiki/Distribui%C3%A7%C3%A3o_uniforme). Todavia, se os dados apresentarem [assimetria](https://pt.wikipedia.org/wiki/Assimetria_(estat%C3%ADstica)) em alguma das direções ou sejam detectados pontos extremos ([outliers](https://pt.wikipedia.org/wiki/Outlier)), pode ser que alguma categoria fique vazia. Para melhor exemplificar esse conceito, utilizei as bibliotecas [Numpy](https://numpy.org/) - para gerar dados amostrados de diferentes distribuições- e a [PySAL](https://pysal.readthedocs.io/en/latest/) - para avaliar diferentes classificadores.

Ao gerar dois <i>datasets</i>, o primeiro a partir de uma [distribuição uniforme](https://docs.scipy.org/doc/numpy/reference/generated/numpy.random.uniform.html) e outro a partir de uma [distribuição log-normal](https://docs.scipy.org/doc/numpy-1.15.1/reference/generated/numpy.random.lognormal.html), foi realizado uma classificação por <span style="color:#AC4142"><strong>intervalos iguais</strong></span> com 5 classes. A figura abaixo, com auxílio dos nossos facilitadores de aprendizagem, ilustra bem os exemplos de casos adequados e inadequados de uso desse tipo de classificador. No histograma da esquerda, temos um padrão de dados bem distribuídos em torno de toda a amplitude, configurando o caso ideal de uso desse tipo de classificador. Ao contrário, no da direita, temos uma distriuição com uma [assimetria positiva](https://pt.wikipedia.org/wiki/Assimetria_(estat%C3%ADstica)), concentrando a maior parte dos valores na primeira classe, além do fato de que uma das classes ficou sem nenhum valor associado.

<center><img src="/images/clf_dados_1/equal_interval_indicacao_corrigido.png"/></center>

Como <span style="color:#AC4142"><strong>vantagem</strong></span> desse tipo de classificação, temos legendas que são mais fáceis de interpretar para audiências não técnicas. No tocante à <span style="color:#AC4142"><strong>desvantagem</strong></span>, para dados com distribuições não uniformes, poderão haver agrupamentos desproporcionais em apenas uma ou duas classes.

### 2. Quebras Naturais (<i>Natural Breaks</i>)

Esse método também é conhecido por Jenks - em homenagem ao inventor [George Frederick Jenks](http://wiki.gis.com/wiki/index.php/George_F._Jenks) - e se utiliza de um algoritmo para minimizar a variação em cada grupo. Assim, quando a informação for apresentada em um mapa, as cores tenderão a aparecer mais distribuídas ao longo de toda visualização. O processo de otimização passa por uma iteração em que o algoritmo busca uma <span style="color:#AC4142"><strong>minimização</strong></span> da variância dentro dos grupos (agrupando os semelhantes), e <span style="color:#AC4142"><strong>maximizando</strong></span> as diferenças entre os grupos (separando os distintos). Além disso, as fronteiras de delimitação das classes são demarcadas nas descontinuidades da distribuição de dados. Portanto, esse método é indicado para ser utilizado em <span style="color:#AC4142"><strong>distribuições não normais e não uniformes</strong></span>. A seguir podemos listar algumas características desse método:

##### VANTAGENS

* Mapear valores que não são igualmente distribuídos ao longo da distribuição, resultando em classes mais balanceadas;
* As classes geradas possuem o máximo possível de homogeniedade interna;

##### DESVANTAGENS

* O mapeamento em classes é inerente ao conjunto de dados em análise, portanto, há uma dificuldade em comparar mapas relacionados a datasets distintos;
* Os resultados são bons apenas se existirem descontinuidades na distribuição de dados;

Para representar o que foi explicado acima, foi utilizado o [NumPy](https://numpy.org/) para criar um amostra de 1000 valores oriundos de uma [distribuição binomial](https://docs.scipy.org/doc/numpy-1.15.0/reference/generated/numpy.random.binomial.html). Por conseguinte, foi realizada a classificação utilizando os métodos de <span style="color:#AC4142"><strong>quebras naturais</strong></span> e <span style="color:#AC4142"><strong>intervalos iguais</strong></span> com 5 classes. A ilustração abaixo apresenta o resultado desse comparativo, onde é possível atestar que a distribuição binomial apresenta algumas descontinuidades. Essa característica configura um dos requisitos de eficácia para o sucesso do algoritmo <span style="color:#AC4142"><strong>Jenks</strong></span>. Como resultado, é possível constatar uma distribuição mais homogênea dos valores entre as 5 classes no histograma da esquerda quando comparado ao da direita.

<center><img src="/images/clf_dados_1/facilitadores_natural_breaks_resized.png"/></center>

Os histogramas acima apresentam as diferenças entre os métodos comparados. Todavia, o impacto dessa classificação para dados apresentados em um mapa é ainda mais relevante. Considere o [Levantamento de Preços e de Margens de Comercialização de Combustíveis](http://www.anp.gov.br/precos-e-defesa-da-concorrencia/precos/levantamento-de-precos) realizado pela [Agência Nacional do Petróleo, Gás Natural e Biocombustíveis (ANP)](http://www.anp.gov.br/). Os mapas abaixo apresentam a <span style="color:#AC4142"><strong>variação acumulada</strong></span> do preço do gás de cozinha (GLP) - em base nominal - entre janeiro de 2013 a junho de 2019. Logo, quando os dados são classificados pelo método de quebras naturais temos um maior número de estados associados as duas últimas categorias. Assim, evidencia-se que estados do Norte e Nordeste tiveram aumentos percentuais maiores que as demais regiões do país. 

<center><img src="/images/clf_dados_1/mapa_natural_break_equal_interval_resized.png"/></center>

### 3. Quantis (<i>Quantiles</i>)

A classificação por quantis tenta alocar um mesmo número de observações por classe. Portanto, conjuntos de dados que estão  <span style="color:#AC4142"><strong>distribuídos de forma homogênea</strong></span> ao longo de toda a distribuição se beneficiam desse tipo de abordagem. A seguir listamos algumas características desse método:

##### VANTAGENS

* É possível enfatizar as posições relativas a determinados valores. Por exemplo, quais observações pertencem aos 20% maiores valores do conjunto de dados?

##### DESVANTAGENS

* Valores que pertecem a uma mesma classe podem ser muito diferentes, particularmente, se os dados não estão distribuídos de forma homogênea ao longo da amplitude;
* O contrário também pode acontecer, que é o caso de observações muitos próximas serem atribuídas a classes distintas.

Para contornar as desvantagens relatadas acima, uma possível abordagem é alterar o número de classes. De modo a apresentar o uso desse método, foi gerada uma amostra com 1000 observações oriundas de uma [distribuição rayleigh](https://docs.scipy.org/doc/numpy-1.15.0/reference/generated/numpy.random.rayleigh.html), alocando esses dados em 5 classes distintas, uma pelo método dos <span style="color:#AC4142"><strong>quantis</strong></span> e outra por <span style="color:#AC4142"><strong>intervalos iguais</strong></span>. A ilustração abaixo apresenta a comparação. Como esperado, o primeiro método distribuiu 200 observações por classe, enquanto o segundo concentra 67% dos valores em apenas duas categorias.

<center><img src="/images/clf_dados_1/tipos_de_classificacao_comparacao_quantile_equal_interval_resized.png"/></center>

É importante realçar a <span style="color:#AC4142"><strong>diferença de abordagem</strong></span> desses dois métodos. A por <span style="color:#AC4142"><strong>quantis</strong></span> se propõe a alocar <u>uma mesma quantidade de observações por classe</u>, independentemente da amplitude dessas. Enquanto a segunda preza pelo estabelecimento de classes com intervalos de mesma grandeza, sem ter o compromisso com o quantitativo de observações vinculadas a cada uma delas. De fato, esse método pode gerar classes sem nenhuma observação vinculada.

A importância de realizar uma <span style="color:#AC4142"><strong>AED</strong></span> de modo a definir a melhor estratégia de classificação é apresentada a seguir. Usamos os dados do [censo de 2010](https://censo2010.ibge.gov.br/) para construir um mapa coroplético da população por município do estado de São Paulo. 

A ilustração abaixo resume os processos realizados até o momento de plotar o mapa. A primeira etapa <span style="color:#AC4142"><strong>[a]</strong></span> consiste na construção de um [strip plot](https://seaborn.pydata.org/generated/seaborn.stripplot.html) para avaliar a distribuição ao longo de toda amplitude. Além disso, é possível constatar que os dados se espalham por mais de sete ordens de grandeza, onde a maior parte deles formam uma nuvem de sobreposições no ínicio da escala. Nesse domínio, destacam-se municípios muito populosos, como o caso de São Paulo.

<center><img src="/images/clf_dados_1/tipo_classificao_populacao_sp_comparativo_homogenous_colors.png"/></center>

Uma abordagem para analisar dados que possuem outliers extremos como os apresentados no gráfico <span style="color:#AC4142"><strong>[a]</strong></span> é fazer uma transformação para uma outra escala, por exemplo, a logarítimica. O gráfico <span style="color:#AC4142"><strong>[b]</strong></span> apresenta o resultado dessa transformação. Desse modo, a distribuição dos dados fica mais evidente, tornando possível identificar o município de Borá que possui o menor número de habitantes registrado naquele censo, com apenas 805 habitantes. Diante disso, foi possível aplicar um método de classificação, como o por quantis, como bem ilustra o histograma do gráfico <span style="color:#AC4142"><strong>[c]</strong></span>. Por fim, foi possível construir o mapa coroplético <span style="color:#AC4142"><strong>[d]</strong></span> com os municípios associados a intervalos populacionais mais adequados.

Demonstramos, até aqui, a importância da escolha adequada de um método de classificação para uma melhor apresentação dos dados. No caso da produção de mapas, os padrões espaciais apresentados serão dependentes do classificador utilizado. Portanto, padrões que existam em um determinado mapa poderão não existir em outro que tenha usado um classificador diferente. Para melhor compreender essas diferenças, observem a ilustração abaixo, que apresenta o uso de diferentes classificadores para um mesmo conjunto de dados. Assim, é possível constatar a diferença nos padrões de mapeamento quando são utilizadas técnicas diferentes.

<center><img src="/images/clf_dados_1/comparativo_tres_classificadores_print.png"/></center>

### 4. Customizado (<i>User defined</i>)

Lembram que mencionei que o conhecimento da regra de negócio associada aos dados é importante? Pois bem: e se o analista julgar que <span style="color:#AC4142"><strong>nenhuma</strong></span> das abordagens tradicionais se aplica ao conjunto de dados em análise? Nesse momento, entrará em campo a <i>expertise</i> de negócio, tanto para customizar as fronteiras entre as classes, quanto para definir a melhor forma de distribuir os dados em intervalos customizados. Portanto, faça uso de todas as suas habilidades como analista e explore diversas técnicas - em seu cinto de utilidades de cientista de dados - <span style="color:#AC4142"><strong>para uma tomada de decisão mais assertiva</strong></span>.

<center><img src="https://media.giphy.com/media/xl3Biy7X0kRlzlQBx4/giphy.gif"/></center>

Assim como proposto, apresentamos 4 abordagens de como classificar dados para construir melhores mapas. Além disso, esse post não esgota todas as opções de classificadores, mas acredito que consiste numa boa introdução a quem deseja compreender as nuances envolvidas na apresentação de dados espaciais. Àqueles que desejam procurar uma fonte de informação para aprofundar seus conhecimentos, indico o livro [Designing Better Maps](https://www.amazon.com.br/Designing-Better-Maps-Guide-Users/dp/1589484401) da autora Cynthia Brewer, a mesma que criou a excelente ferramenta [Color Brewer](http://colorbrewer2.org/).

Por fim, mas não menos importante, gostaria de agradecer aos meu amigos <strong>[Roberto Mourão](https://www.linkedin.com/in/rnmourao/)</strong>,  <strong>[Paulo Haddad](https://www.linkedin.com/in/paulochf/)</strong>, <strong>[Fernando Barbalho](https://www.linkedin.com/in/fernando-almeida-barbalho-00623640/)</strong></span> e <strong>[Romualdo Alves](https://www.linkedin.com/in/romualdoalves/)</strong> pelas valiosas contribuições a esse texto. Fica aqui o meu muito-obrigado!

`E aí gostou do post? Tem alguma sugestão ou dúvida? Deixe um comentário e até a próxima!`

