# Hipóteses e padrões

Antes de implementar qualquer algoritmo de machine learning, precisamos entender minimamente o que são hipóteses e como elas influenciam a busca por um padrão _bom_(?) de solução. Lembra do exemplo dos exames e da doença que demos aula passada? Vamos modificá-lo um pouco para podermos desenhar em <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{R}^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{R}^2" title="\mathbb{R}^2" /></a>

Considere a seguinte tabela de dados:

|Exame 1| Exame 2| Doente? |
|-------|------- |---------|
| 30    | 10     | Não     |   
| 30    | 20     | Não     |   
| 40    | 30     | Sim     |
| 45    | 40     | Sim     |
| 50    | 50     | Sim     |
| 30    | 30     | Não     |
| 15    | 40     | Não     |

##### Como plotamos os dados?
Boa pergunta. A maneira mais convencional é considerar cada tipo de dado como uma dimensão. Ou seja, no caso acima, teríamos duas dimensões: Exame 1 e Exame 2. A classificação (Doente?) serve apenas para iteração do algoritmo, não costumamos plotá-lo para diminuir o grau de complexidade da visualização, afinal, estaríamos plotando uma dimensão a mais. Veremos que, apenas plotando os dados, conseguimos uma maneira inteligente de dividi-los sem precisar plotar sua devida classificação: faremos isso pintando eles de uma determinada cor. No caso acima, por exemplo, poderíamos pintar os saudáveis de azul e os doentes de vermelho.

![](./img/plot1.png)
<br><br>

Não se esqueça do nosso objetivo inicial: separar os doentes dos não doentes. Se você tivesse que escolher uma função, ou algum tipo de curva que os separasse, qual escolheria?

###### Ah, existem infinitas curvas que separam esses dados. A mais simples de todas é uma reta, mas eu quero uma parábola porque sim.

Tudo bem, vamos escolher alguma parábola que separe esses dados. Uma possível parábola que separa os dados é:
 <a href="https://www.codecogs.com/eqnedit.php?latex=-x^2&plus;83x&plus;4y=1800" target="_blank"><img src="https://latex.codecogs.com/gif.latex?-x^2&plus;83x&plus;4y=1800" title="-x^2+83x+4y=1800" /></a>

(A equação é irrelevante para o entendimento do que queremos, não se assuste)
<br><br>

![](./img/plot2.png)

Bom, você concorda comigo que poderíamos ter escolhido simplesmente uma reta?

###### Sim, é mais simples, mas quem garante que é melhor?

Olha, garantir eu não posso, mas tenho razões para te fazer acreditar que a chance de eu estar certo é maior que a sua. Mas, para formalizar isso, precisamos construir alguns conceitos.
<br><br>

#### Erro
Primeiramente, lembra da aula passada que eu disse que podemos ter algum erro dentro da amostra, e ainda sim não é o fim do mundo?

#### Peraí, peraí. Por que temos erro dentro da amostra se já sabemos previamente a classificação dos dados?

Excelente pergunta! Porque quem vai nos responder a classificação do dado é o algoritmo, nós apenas vamos programá-lo. Nós podemos arbitrariamente pegar os dados que ele classificou errado e mudar para obter erro 0 dentro da amostra, mas estaríamos fazendo com que ele *decorasse* esse dado, isto é, ele não seria fruto do resultado de um algoritmo de machine learning.  

Voltando, uma vez que rodamos nosso algoritmo de classificação, uma das coisas a serem avaliadas é a função erro. Há dois tipos de erro:

**1) Erro dentro da amostra**: denotado por <a href="https://www.codecogs.com/eqnedit.php?latex=E_i_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_i_n" title="E_i_n" /></a>, para calculá-lo no caso de um problema de classificação, contaremos quantos dados nosso algoritmo classificou errado. Para isso, basta iterar sobre todos os nossos dados, comparar a **classificação real** com a devolvida pelo nosso algoritmo e ver se são iguais. Em suma, <a href="https://www.codecogs.com/eqnedit.php?latex=E_i_n=\frac{\&hash;incorretos}{\&hash;total}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_i_n=\frac{\&hash;incorretos}{\&hash;total}" title="E_i_n=\frac{\#incorretos}{\#total}" /></a>

**2) Erro fora da amostra**: denotado por <a href="https://www.codecogs.com/eqnedit.php?latex=E_o_u_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_o_u_t" title="E_o_u_t" /></a>, representa os dados que foram classficados incorretamente na tentativa de generalização. É **impossível** calculá-lo. Pensa comigo: se soubessemos como cálculá-lo, saberíamos mudar nossa classificação para correta, e _voilà_, sabemos classificar todos os dados do mundo corretamente.

#### Mas você não acabou de dizer que mudar a classificação manualmente é decorar?
Sim, mas há uma sutil diferença: no caso anterior estávamos dentro da amostra, e o motivo pelo qual decorar dentro da amostra é ruim porque diminui a chance de generalização, isto é, quando decoramos aumentamos <a href="https://www.codecogs.com/eqnedit.php?latex=E_o_u_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_o_u_t" title="E_o_u_t" /></a>. O único caso em que decorar seria bom é caso pudéssemos fazê-lo com todos os dados daquela situação, o que é completamente inviável.

 Em um problema de classificação, que é nosso caso, o erro é binário: ou eu acerto, ou eu erro. Mas veremos, mais para frente, que é possível definir outros tipos de erro.

#### Hipóteses
Mesmo que você não saiba me dizer qual a solução certa, você é capaz de me dizer a **família** de soluções que seu algoritmo devolve. Por exemplo, você me deu uma parábola como solução, ou seja, seu algoritmo tem como saída equações do segundo grau como soluções. Já o meu sempre devolve retas. Quais as diferenças básicas?

Antes de responder isso, vamos tentar formalizar um pouco o que é uma **hipótese**. Nosso algoritmo resolve um problema de classificação em diferentes **categorias**. Particularmente, no exemplo dado anteriormente as categorias são binárias: doente ou não doente. Existe uma função matemática <a href="https://www.codecogs.com/eqnedit.php?latex=f:\mathbb{R}^n\rightarrow\mathbb{R}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f:\mathbb{R}^n\rightarrow\mathbb{R}" title="f:\mathbb{R}^n\rightarrow\mathbb{R}" /></a> que separa **100% corretamente** todos os dados **fora e dentro da amostra**, porém ela é **desconhecida** e **inatingível**. O domínio dela é uma tupla contendo em cada coordenada um tipo de dado fornecido, por exemplo, <a href="https://www.codecogs.com/eqnedit.php?latex=(Exame_1,Exame_2,Exame_3...)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(Exame_1,Exame_2,Exame_3...)" title="(Exame_1,Exame_2,Exame_3...)" /></a> (por isso <a href="https://www.codecogs.com/eqnedit.php?latex=\mathbb{R}^n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbb{R}^n" title="\mathbb{R}^n" /></a>) e seu contra-domínio devolve sua classificação, que em geral é um número inteiro, mas nada impede que seja real. Porém, não temos informação o suficiente para construí-la, portanto, o que fazemos com machine learning é tentar aprender um padrão, **encontrar uma hipótese que se aproxime o máximo possível da realidade**.

Agora que formalizamos, vamos voltar à pergunta inicial: quais as diferenças entre o seu algoritmo, que tem como saída equações do segundo grau, e o meu, que devolve do primeiro grau?
<br><br>
 O seu fornece soluções da forma <a href="https://www.codecogs.com/eqnedit.php?latex=ax^2&plus;bx&plus;c" target="_blank"><img src="https://latex.codecogs.com/gif.latex?ax^2&plus;bx&plus;c" title="ax^2+bx+c" /></a>, enquanto que o meu somente <a href="https://www.codecogs.com/eqnedit.php?latex=ax&plus;b" target="_blank"><img src="https://latex.codecogs.com/gif.latex?ax&plus;b" title="ax+b" /></a>. Faça <a href="https://www.codecogs.com/eqnedit.php?latex=a=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?a=0" title="a=0" /></a> na equação do segundo grau, obtemos <a href="https://www.codecogs.com/eqnedit.php?latex=bx&plus;c" target="_blank"><img src="https://latex.codecogs.com/gif.latex?bx&plus;c" title="bx+c" /></a> , que é essencialmente uma equação de reta, concorda? Isto significa que seu algoritmo também pode devolver retas como soluções, ou seja, o **conjunto de hipóteses do seu algoritmo engloba o do meu**.
<br><br>

##### Então, teoricamente, o meu é melhor, já que toda saída que o seu dá, o meu também poderia dar, certo?

Errado! Calma, você está está certo em dizer que o seu devolve tudo o que o meu poderia devolver e mais um pouco, porém errado ao dizer que é melhor por isso, **é justamente o contrário**. Nas próximas aulas provaremos isso, mas guarde isso com carinho: **quanto maior seu conjunto de hipóteses, menos chances temos de garantir que estamos certo**. Caso não tenha contato profundo ou nem mesmo superficial (principalmente se for esse o caso) com probabilidade e estatística, preste bastante atenção nisto: eu disse **chances** de estar certo. Sim, chances têm tudo a ver com probabilidades. Considere a seguinte fórmula, uma pequena variação da conhecida (nos campos da probabilidade) desigualdade de Hoeffding:
<br>

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<a href="https://www.codecogs.com/eqnedit.php?latex=P[|E_i_n&space;-&space;E_o_u_t|>\varepsilon]&space;\leq&space;2Me^{-2\varepsilon^2N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P[|E_i_n&space;-&space;E_o_u_t|>\varepsilon]&space;\leq&space;2Me^{-2\varepsilon^2N}" title="P[|E_i_n - E_o_u_t|>\varepsilon] \leq 2Me^{-2\varepsilon^2N}" /></a>

Calma, não se assuste, vou explicar cada detalhe dela, mas não vamos prová-la, pois exigiria uma boa carga de probabilidade e estatística envolvida, apenas vamos partir da desigualdade de Hoeffding original e mostrar como chegamos nessa variação acima, mas isso em aulas futuras.

Vamos definir o que cada parâmetro significa:

* <a href="https://www.codecogs.com/eqnedit.php?latex=E_i_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_i_n" title="E_i_n" /></a> e <a href="https://www.codecogs.com/eqnedit.php?latex=E_o_u_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_o_u_t" title="E_o_u_t" /></a>

  Como visto anteriormente, representam, respectivamente, os erros dentro e fora da amostra.

* <a href="https://www.codecogs.com/eqnedit.php?latex=N" target="_blank"><img src="https://latex.codecogs.com/gif.latex?N" title="N" /></a>

  Representa a quantidade de dados que nós dispomos. No caso dos exames, temos 7 dados, portanto, N = 7

* <a href="https://www.codecogs.com/eqnedit.php?latex=M" target="_blank"><img src="https://latex.codecogs.com/gif.latex?M" title="M" /></a>

  Representa o número de hipóteses do nosso modelo. Por enquanto ainda não sabemos calcular M para ambos os casos anteriores (parábola e reta), pois são infinitos. Mas, por enquanto, basta saber que o primeiro é maior que o segundo. Faremos uma análise puramente qualitativa desta desigualdade.

* <a href="https://www.codecogs.com/eqnedit.php?latex=\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varepsilon" title="\varepsilon" /></a>

  É a única variável dentre nossos parâmetros. Se você me der um <a href="https://www.codecogs.com/eqnedit.php?latex=\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varepsilon" title="\varepsilon" /></a>, eu te dou uma probabilidade associada.

<br>
Agora, vamos analisar cada parte da fórmula:

* <a href="https://www.codecogs.com/eqnedit.php?latex=P[|E_i_n-E_o_u_t|>\varepsilon]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P[|E_i_n-E_o_u_t|>\varepsilon]" title="P[|E_i_n-E_o_u_t|>\varepsilon]" /></a>

  Estamos analisando o módulo da diferença entre o erro dentro e fora da amostra. Lembra que eu disse que era impossível calcular <a href="https://www.codecogs.com/eqnedit.php?latex=E_o_u_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_o_u_t" title="E_o_u_t" /></a>? Essa é uma maneira de estimá-lo, já que estamos calculando a probabilidade de <a href="https://www.codecogs.com/eqnedit.php?latex=E_o_u_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_o_u_t" title="E_o_u_t" /></a> estar tão próximo quanto eu queira, a depender da escolha de <a href="https://www.codecogs.com/eqnedit.php?latex=\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varepsilon" title="\varepsilon" /></a>.

* <a href="https://www.codecogs.com/eqnedit.php?latex=2Me^{-2\varepsilon^2N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?2Me^{-2\varepsilon^2N}" title="2Me^{-2\varepsilon^2N}" /></a>

  É o limite superior para a probabilidade, isto é, a chance de <a href="https://www.codecogs.com/eqnedit.php?latex=|E_i_n-E_o_u_t|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?|E_i_n-E_o_u_t|" title="|E_i_n-E_o_u_t|" /></a> ser maior que <a href="https://www.codecogs.com/eqnedit.php?latex=\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varepsilon" title="\varepsilon" /></a> é menor ou igual a esse cara aí em cima.

<br>

No mundo ideal, eu quero que a probabilidade de <a href="https://www.codecogs.com/eqnedit.php?latex=E_i_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_i_n" title="E_i_n" /></a> estar muito próximo de <a href="https://www.codecogs.com/eqnedit.php?latex=E_o_u_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?E_o_u_t" title="E_o_u_t" /></a> seja muito alta. Em outras palavras, quero que <a href="https://www.codecogs.com/eqnedit.php?latex=P[|E_i_n-E_o_u_t|>\varepsilon]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P[|E_i_n-E_o_u_t|>\varepsilon]" title="P[|E_i_n-E_o_u_t|>\varepsilon]" /></a> seja muito pequeno. Porém, repare que, quanto menor for a escolha de <a href="https://www.codecogs.com/eqnedit.php?latex=\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varepsilon" title="\varepsilon" /></a>, menos eu consigo limitar, pois do lado direito temos uma exponencial negativa, isto é, quanto menor o <a href="https://www.codecogs.com/eqnedit.php?latex=\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\varepsilon" title="\varepsilon" /></a>, maior o valor, portanto, dá uma probabilidade alta dos erros estarem distantes, **o que não significa que, na prática, estão**.

Finalizando a ideia, lembra que eu disse que te daria algumas razões para acreditar que uma reta era uma escolha melhor do que uma parábola? Pois bem,  <a href="https://www.codecogs.com/eqnedit.php?latex=M_r_e_t_a<M_p_a_r_a_b_o_l_a" target="_blank"><img src="https://latex.codecogs.com/gif.latex?M_r_e_t_a<M_p_a_r_a_b_o_l_a" title="M_r_e_t_a<M_p_a_r_a_b_o_l_a" /></a>, portanto, <a href="https://www.codecogs.com/eqnedit.php?latex=P[|E_i_n-E_o_u_t|>\varepsilon]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P[|E_i_n-E_o_u_t|>\varepsilon]" title="P[|E_i_n-E_o_u_t|>\varepsilon]" /></a> é **menos limitado** pela desigualdade.
