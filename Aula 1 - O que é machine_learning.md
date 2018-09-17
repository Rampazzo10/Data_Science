# O que é machine learning?

   Antes de ensinar algoritmos de aprendizado de máquina, precisamos definir, **precisamente**, como ensinamos algo a um computador. Uma resposta intuitiva seria que após rodado o algoritmo, o computador fosse capaz de responder perguntas. É uma resposta **quase** correta, futuramente voltaremos nesse ponto.

  ##### Quando usar machine learning?  
   Primeiramente é importante definir nosso escopo de trabalho. Quando falamos de aprendizado de máquina, é imprescindível que tenhamos um conjunto de **dados**. A regra é simples: *no data => no machine learning*</p>
   <p>Ah, e claro, precisamos supor que nossos dados estão dentro de algum padrão, por mais bizarro que ele seja. Porque se for, de fato, aleatório, por uma questão de lógica não tem o que aprender, afinal, é aleatório.</p>

   ##### Mas como diferenciar se estamos ensinando ela a *aprender* ou a *decorar*?

   <p>Machine learning é bastante usado em problemas de classificação de dados. Imagine que você recebeu o resultado de um exame que forneça a concentração de uma substância no seu organismo e deseja, a partir dela, dar um veredito se o paciente está ou não doente. Nesse caso, meus dados seriam a seguinte tabela:</p>

  | Exame | Doente? |
  |-------|---------|
  | 10    | Sim     |   
  | 20    | Sim     |   
  | 30    | Não     |
  | 40    | Não     |
  | 50    | Não     |
  | 60    | Sim     |
  | 70    | Sim     |

  A coluna de **Exame** representa meu dado (ou seja, neste caso é unidimensional), enquanto que **Doente?** representa sua classificação. Consegue perceber um padrão nos dados? Pois é, nem eu. Mas como bons técnicos, sabemos (não ainda) treinar o computador para que ele aprenda um **possível** padrão nos dados.

  ##### Ué, mas o que garante que o padrão encontrado pelo computador é o correto?

  Excelente pergunta. Repare que fui bem preciso ao dizer **possível** padrão. Você dispõe de um conjunto de dados e quer inferir algo a partir deles, o que não significa que a inferência é verossímil.

  ##### Mas isso significa que nossa técnica então não é muito boa, não é?


  De forma alguma. Nós apenas tentando responder uma pergunta que não tem gabarito. Não existe o **padrão correto**. Existem padrões **melhores**, e futuramente mostraremos como buscá-los. Se soubéssemos a resposta correta, uma função matemática que separa seus dados, não faz sentido usar machine learning.

  Segundo o Professor Yasser da Universidade de Caltech, enquanto o aprendizado está ocorrendo, tudo o que você precisa fazer é sentar e tomar um chá enquanto seu computador aprende. Formalmente falando, precisamos conceber uma maneira de factualmente **ensinar** uma máquina. Está faltando apenas um pequeno detalhe. Lembra que eu falei que nossa definição de machine learning estava quase correta? Mas por que quase? Porque há uma grande diferença entre aprender e decorar, e isso está muito associada à técnica de buscar padrões de resposta melhores: uma resposta tipicamente decorada está longe de ser um padrão bom.

  ##### Mas como eu identifico se estou ensinando o computador a decorar ou aprender?

  Primeiramente vamos ver um exemplo prático do que seria decorar. Imagina que ao invés de usar um algoritmo de aprendizado para resolver nosso problema dos exames, eu resolvo-o da seguinte maneira: eu, **arbitrariamente**, digo que os únicos doentes são os apresentados na amostra, e qualquer outro indivíduo testado será classificado como **não doente**.

  ###### Mas essa "função" que chegamos estaria errada?

  Não. Volto a dizer: nunca podemos dizer se nossa resposta final é certa, porque não temos gabarito. Mas eu te afirmo: a chance de ela estar certa é muito baixa, e apesar de você não saber exatamente o porquê, tenho certeza que você tem esse sentimento de que essa hipótese nos parece ruim. Fique tranquilo, alguma hora provaremos que, de fato, ela é uma má candidata a função padrão.
   Agora, voltando à pergunta anterior. Eu gosto de pensar de duas maneiras para diferenciar **decorar** de **aprender**:<br>
  **1) Intuição:** quando ocorre o que chamamos de **data snooping**, que seria literalmente espiar os dados. No caso acima dizemos que 10, 20, 60 e 70 para valores de Exame 1 são doentes. Mas como chegamos a essa conclusão? Espiamos os dados e montamos um modelo baseado neles. Data snooping prejudica a **generalização** da sua hipótese <br><br>
  **2) Falta de generalização:** quando nos preocupamos muito em acertar dentro da amostra, reduzimos a chance de acertar fora, justamente porque estamos **forçando** que o algoritmo classfique a amostra de modo 100% correto. Repare que eu não estou dizendo que ter erro 0 dentro da amostra é ruim, mas apenas que não é o fim do mundo se não tivermos, inclusive pode até ser melhor.

  ###### Qual a utilidade de machine learning? Se vamos ensinar o computador a resolver, significa que já sabemos, certo?

  Errado. Nós vamos desenvolver uma maneira de **treinar** um computador. É como se fôssemos um técnico de futebol ou coaching profissional: sabemos bem a teoria, mas deixa a prática pra quem tem maior capacidade e "energia" (e quer mais velocidade/capacidade de executar um algoritmo que um computador??). Nós sabemos o *caminho das pedras* para resolver o problema, mas não temos a resposta.

  ##### E como implementamos um algoritmo de machine learning?
  Aguarde os próximos capítulos...
