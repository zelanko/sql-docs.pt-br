---
title: "Compatibilidade de fórmula do DAX no modo DirectQuery (SSAS 2016) | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d2fbafe6-d7fb-437b-b32b-fa2446023fa5
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d7c13126b258662572b5ad5a9b02bcf7921c2346
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dax-formula-compatibility-in-directquery-mode"></a>Compatibilidade de fórmulas DAX no modo DirectQuery 
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

1200 e superior para modelos de tabela no modo DirectQuery, muitas limitações funcionais em versões anteriores não se aplicarão mais. Especificamente para as fórmulas DAX:

- O DirectQuery agora gera consultas mais simples, fornecendo melhor desempenho.
- Agora há suporte para a segurança em nível de linha (RLS) no modo DirectQuery.
- Colunas calculadas agora têm suporte para modelos de tabela no modo DirectQuery.

## <a name="dax-functions-in-directquery-mode"></a>Funções DAX no modo DirectQuery

Em resumo, todas as funções DAX têm suporte para modelos DirectQuery. No entanto, nem todas as funções têm suporte para todos os tipos de fórmula, e nem todas as funções foram otimizadas para modelos DirectQuery. Nível mais básico, podemos separar as funções DAX em dois grupos: otimizadas e não otimizadas. Primeiro, vamos examinar com mais detalhes as funções otimizadas.


### <a name="optimized-for-directquery"></a>Otimizada para DirectQuery
Essas são funções que retornam principalmente resultados de agregação ou escalares. Essas funções são divididas entre aquelas que têm suporte em todos os tipos de fórmulas: medidas, consultas, colunas calculadas, segurança em nível de linha e aquelas que têm suporte somente em fórmulas de medida e de consulta. Eles incluem:    

| Com suporte em todas as fórmulas DAX                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Com suporte apenas em fórmulas de medida e de consulta                                                                                                                                                                                                                                                                                                |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ABS</br>  ACOS</br>  ACOT</br>  AND</br>  ASIN</br>  ATAN</br>  BLANK</br>  CEILING</br>  CONCATENATE</br>  COS</br>  COT</br>  CURRENCY</br>  DATE</br>  DATEDIFF</br>  DATEVALUE</br>  DAY</br>  DEGREES</br>  DIVIDE</br>  EDATE</br>  EOMONTH</br>  EXACT</br>  EXP</br>  FALSE</br>  FIND</br>  HOUR</br>  IF</br>  INT</br>  ISBLANK</br>  ISO.CEILING</br>  KEEPFILTERS</br>  LEFT</br>  LEN</br>  LN</br>  LOG</br>  LOG10</br>  LOWER</br>  MAX</br>  MID</br>  MIN</br>  MINUTE</br>  MOD</br>  MONTH</br>  MROUND</br>  NOT</br>  NOW</br>  OU</br>  PI</br>  POWER</br>  QUOTIENT</br>  RADIANS</br>  RAND</br>  RELATED</br>  REPT</br>  RIGHT</br>  ROUND</br>  ROUNDDOWN</br>  ROUNDUP</br>  SEARCH</br>  SECOND</br>  SIGN</br>  SIN</br>  SQRT</br>  SQRTPI</br>  SUBSTITUTE</br>  SWITCH</br>  TAN</br>  TIME</br>  TIMEVALUE</br>  TODAY</br>  TRIM</br>  TRUE</br>  TRUNC</br>  UNICODE</br>  UPPER</br>  USERNAME</br>  USERELATIONSHIP</br>  VALUE</br>  WEEKDAY</br>  WEEKNUM</br>  YEAR</br> | ALL</br> ALLEXCEPT</br> ALLNOBLANKROW</br> ALLSELECTED</br> AVERAGE</br> AVERAGEA</br> AVERAGEX</br> CALCULATE</br> CALCULATETABLE</br> COUNT</br> COUNTA</br> COUNTAX</br> COUNTROWS</br> COUNTX</br> DISTINCT</br> DISTINCTCOUNT</br> FILTER</br> FILTERS</br> HASONEFILTER</br> HASONEVALUE</br> ISCROSSFILTERED</br> ISFILTERED</br> MAXA</br> MAXX</br> MIN</br> MINA</br> MINX</br> RELATEDTABLE</br> STDEV.P</br> STDEV.S</br> STDEVX.P</br> STDEVX.S</br> SUM</br> SUMX</br> VALUES</br> VAR.P</br> VAR.S</br> VARX.P</br> VARX.S |



### <a name="non-optimized-for-directquery"></a>Não otimizada para DirectQuery
Essas funções não foram otimizadas para trabalhar com o DirectQuery. Essas funções *não têm* nenhum suporte em fórmulas de coluna calculada e de segurança em nível de linha. No entanto, essas funções *têm suporte* em fórmulas de medida e de consulta, embora com desempenho duvidoso.

 Não listaremos todas as funções aqui. Basicamente, se ela não estiver em uma das listas de funções otimizadas acima, será uma função não otimizada para DirectQuery.

Os motivos de uma função específica não ser otimizada para DirectQuery é porque o mecanismo relacional subjacente não pode executar cálculos equivalentes àqueles executados pelo mecanismo xVelocity, ou então a fórmula não pode ser convertida em uma expressão SQL equivalente. Em outros casos, o desempenho da expressão convertida e dos cálculos resultantes poderia ser inaceitável.

Para saber mais sobre todas as funções DAX, consulte a [Referência de função DAX]. (https://msdn.microsoft.com/en-us/library/ee634396.aspx)

## <a name="dax-operators-in-directquery-mode"></a>Operadores DAX no modo DirectQuery
Todos os operadores de comparação e de aritmética DAX têm suporte total no modo DirectQuery. Para obter mais informações, consulte [Referência de operador DAX](https://msdn.microsoft.com/library/ee634237.aspx).


 
## <a name="differences-between-in-memory-and-directquery-mode"></a>Diferenças entre os modos na memória e DirectQuery  
Consultas em um modelo implantado no modo DirectQuery podem retornar resultados diferentes do mesmo modelo implantado no modo na memória. Isso porque, com o DirectQuery, os dados são consultados diretamente de um armazenamento de dados relacional, e agregações necessárias para fórmulas são executadas com o mecanismo relacional relevante em vez de usar o mecanismo analítico xVelocity (VertiPaq) na memória para armazenamento e cálculo.  
  
Por exemplo, há diferenças no modo como certos repositórios de dados relacionais tratam valores numéricos, datas, nulos etc.  
  
Em contrapartida, a linguagem DAX destina-se a emular, do modo mais semelhante possível, o comportamento das funções no Microsoft Excel. Por exemplo, ao tratar nulos, cadeias de caracteres vazias e valores de zero, o Excel tenta fornecer a melhor resposta, independentemente do tipo de dados preciso e, portanto, o mecanismo xVelocity faz o mesmo. No entanto, quando um modelo tabular é implantado no modo DirectQuery e passa fórmulas a uma fonte de dados relacional, os dados devem ser tratados de acordo com a semântica da fonte de dados relacional, o que geralmente requer o tratamento distinto de cadeias de caracteres e nulos. Por isso, a mesma fórmula pode retornar um resultado diferente quando avaliada em relação aos dados armazenados em cache e em relação aos dados retornados exclusivamente do repositório relacional.  
  
Além disso, algumas funções não foram otimizadas para o modo DirectQuery, pois o cálculo exigiria que os dados no contexto atual fossem enviados à fonte de dados relacionais como um parâmetro. Por exemplo, medidas que usam funções de inteligência de tempo que fazem referência a intervalos de datas em uma tabela de calendário. Uma fonte de dados relacional não pode ter uma tabela de calendário ou pelo menos uma com .  
  
## <a name="semantic-differences"></a>Diferenças semânticas  
Esta seção lista os tipos de diferenças semânticas que você pode esperar e descreve as limitações que podem se aplicar ao uso de funções ou aos resultados da consulta.  
  
### <a name="comparisons"></a>Comparações  
A DAX nos modelos na memória dá suporte a comparações de duas expressões que são resolvidas para valores escalares de tipos de dados diferentes. No entanto, modelos implantados no modo DirectQuery usam os tipos de dados e os operadores de comparação do mecanismo relacional e, portanto, podem retornar resultados diferentes.  
  
As seguintes comparações sempre retornarão um erro quando usadas em um cálculo em uma fonte de dados DirectQuery:  
  
-   Tipo de dados numeric comparado a qualquer tipo de dados string  
  
-   Tipo de dados numeric comparado a um valor booliano  
  
-   Qualquer tipo de dados string comparado a um valor booliano  
  
Em geral, a DAX é mais tolerante com incompatibilidades de tipo de dados em modelos na memória e tentará uma conversão implícita de valores até duas vezes, conforme descrito nesta seção. No entanto, as fórmulas enviadas a um repositório de dados relacional no modo DirectQuery são avaliadas com mais rigor, de acordo com as regras do mecanismo relacional e apresentam maior probabilidade de falha.  
  
**Comparações de cadeias de caracteres e números**  
EXEMPLO: `“2” < 3`  
  
A fórmula compara uma cadeia de caracteres de texto a um número. A expressão é **true** no modo DirectQuery e em modelos na memória.  
  
Em um modelo na memória, o resultado é **true** porque números como cadeias de caracteres são convertidos implicitamente em um tipo de dados numérico para comparações com outros números. O SQL também converte implicitamente números de texto como números para comparação com tipos de dados numéricos.  
  
Observe que isso representa uma alteração no comportamento da primeira versão do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], que retornaria **false**, pois o texto “2” sempre seria considerado maior do que qualquer número.  
  
**Comparação de texto com booliano**  
EXEMPLO: `“VERDADERO” = TRUE`  
  
Esta expressão compara uma cadeia de caracteres de texto com um valor booliano. Em geral, para modelos DirectQuery ou Na Memória, a comparação de um valor de cadeia de caracteres com um valor booliano resulta em um erro. As únicas exceções à regra ocorrem quando a cadeia de caracteres contém as palavras **true** ou **false**; se a cadeia de caracteres contiver um dos valores true ou false, uma conversão em booliano será feita e a comparação ocorrerá, apresentando o resultado lógico.  
  
**Comparação de nulos**  
EXEMPLO: `EVALUATE ROW("X", BLANK() = BLANK())`  
  
Esta fórmula compara o SQL equivalente de um nulo a um nulo. Retorna **true** em modelos na memória e DirectQuery; um provisionamento é feito no modelo DirectQuery para garantir comportamento semelhante a um modelo na memória.  
  
Observe que, no Transact-SQL, um nulo nunca é igual a um nulo. No entanto, na DAX, um espaço em branco é igual a outro espaço em branco. Esse comportamento é o mesmo para todos os modelos na memória. É importante observar que o modo DirectQuery usa grande parte da semântica do SQL Server; mas, nesse caso, se separa dela, proporcionando um novo comportamento a comparações NULL.  
  
### <a name="casts"></a>Conversões  
  
Não há nenhuma função de conversão como na DAX, mas conversões implícitas são executadas em muitas operações de comparação e aritméticas. É a operação de comparação ou aritmética que determina o tipo de dados do resultado. Por exemplo,  
  
-   Valores boolianos são tratados como numéricos em operações aritméticas, como TRUE + 1, ou a função MIN aplicada a uma coluna de valores boolianos. Uma operação NOT também retorna um valor numérico.  
  
-   Valores boolianos sempre são tratados como valores lógicos em comparações e quando usados com EXACT, AND, OR, &amp;&amp;ou ||.  
  
**Conversão de cadeia de caracteres em booliano**  
Em modelos na memória e DirectQuery, são permitidas conversões em valores boolianos destas cadeias de caracteres apenas: **“”** (cadeia de caracteres vazia), **“true”**, **“false”**; em que uma cadeia de caracteres vazia é convertida em um valor falso.  
  
As conversões no tipo de dados Boolean de qualquer outra cadeia de caracteres resultam em um erro.  
  
**Conversão de cadeia de caracteres em data/hora**  
No modo DirectQuery, conversões de representações de cadeias de caracteres de datas e horas em valores **datetime** reais apresentam o mesmo comportamento que teriam no SQL Server.   
  
Os modelos que usam o repositório de dados na memória oferecem suporte a um intervalo mais limitado de formatos de texto para datas que os formatos de cadeias de caracteres para datas que têm suporte no SQL Server. No entanto, a DAX oferece suporte a formatos de data e hora personalizados.  
  
**Conversão de cadeia de caracteres em outros valores não boolianos**  
Ao converter de cadeias de caracteres em valores não boolianos, o modo DirectQuery se comporta da mesma forma que no SQL Server. Para obter mais informações, veja [CAST e CONVERT (Transact-SQL)](http://msdn.microsoft.com/en-us/a87d0850-c670-4720-9ad5-6f5a22343ea8).  
  
**Não é permitido converter de números em cadeia de caracteres**  
EXEMPLO: `CONCATENATE(102,”,345”)`  
  
A conversão de números em cadeias de caracteres não é permitida no SQL Server.  
  
Esta fórmula retorna um erro em modelos tabulares e no modo DirectQuery; no entanto, a fórmula produz um resultado no [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].  
  
**Não há suporte para conversões em duas tentativas no DirectQuery**  
Com frequência, os modelos na memória tentam uma segunda conversão quando a primeira falha. Isso nunca acontece no modo DirectQuery.  
  
EXEMPLO: `TODAY() + “13:14:15”`  
  
Nessa expressão, o primeiro parâmetro tem o tipo **datetime** e o segundo tem o tipo **string**. No entanto, as conversões durante a combinação dos operandos são tratadas de modo diferente. A DAX executará uma conversão implícita de **string** em **double**. Nos modelos na memória, o mecanismo da fórmula tentará converter diretamente em **double**e, se falhar, tentará converter a cadeia de caracteres em **datetime**.  
  
No modo DirectQuery, somente a conversão direta de **string** em **double** será aplicada. Se essa conversão falhar, a fórmula retornará um erro.  
  
### <a name="math-functions-and-arithmetic-operations"></a>Funções matemáticas e operações aritméticas  
Algumas funções matemáticas retornarão resultados diferentes no modo DirectQuery, devido às diferenças no tipo de dados subjacente ou as conversões que podem ser aplicadas em operações. Além disso, as restrições descritas acima no intervalo de valores permitido poderão afetar o resultado das operações aritméticas.  
  
**Ordem de adição**  
Quando você cria uma fórmula que adiciona uma série de números, um modelo na memória pode processar os números em uma ordem diferente da de um modelo DirectQuery.  Portanto, quando há muitos números positivos muito grandes e números negativos muito grandes, você pode receber um erro em uma operação e resultados em outra.  
  
**Uso da função POWER**  
EXEMPLO: `POWER(-64, 1/3)`  
  
No modo DirectQuery, a função POWER não pode usar valores negativos como a base, quando elevada a um expoente fracionário. Esse é o comportamento esperado no SQL Server.  
  
Em um modelo na memória, a fórmula retorna -4.  
  
**Operações de estouro numéricas**  
No Transact-SQL, as operações que resultam em um estouro numérico retornam um erro de estouro; portanto, fórmulas que resultam em um estouro também geram um erro no modo DirectQuery.  
  
No entanto, quando usada em um modelo na memória, a mesma fórmula retorna um número inteiro de oito bytes. Isso ocorre porque o mecanismo da fórmula não executa verificações de estouros numéricos.  
  
**Funções LOG com espaços em branco retornam resultados diferentes**  
O SQL Server trata nulos e espaços em branco de modo diferente do mecanismo xVelocity. Com isso, a fórmula a seguir retorna um erro no modo DirectQuery, mas retorna infinito no modo (-inf) na memória.  
  
`EXAMPLE: LOG(blank())`  
  
As mesmas limitações se aplicam a outras funções logarítmicas: LOG10 e LN.  
  
Para obter mais informações sobre o tipo de dados **blank** na DAX, consulte [Referência de sintaxe DAX](https://msdn.microsoft.com/library/ee634217.aspx).  
  
**Divisão por 0 e divisão por espaço em branco**  
No modo DirectQuery, a divisão por zero (0) ou a divisão por BLANK sempre resultará em um erro. O SQL Server não oferece suporte à noção de infinito e, como o resultado natural de qualquer divisão por 0 é infinito, o resultado é um erro. No entanto, o SQL Server oferece suporte à divisão por nulos e o resultado sempre deve ser igual a nulo.  
  
Em vez de retornar resultados diferentes para essas operações, no modo DirectQuery, ambos os tipos de operações (divisão por zero e divisão por nulo) retornam um erro.  
  
Observe que, em modelos do Excel e do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , a divisão por zero também retorna um erro. A divisão por um espaço em branco retorna um espaço em branco.  
  
As seguintes expressões são válidas em modelos na memória, mas falharão no modo DirectQuery:  
  
`1/BLANK`  
  
`1/0`  
  
`0.0/BLANK`  
  
`0/0`  
  
A expressão `BLANK/BLANK` é um caso especial que retorna `BLANK` em modelos na memória e no modo DirectQuery.  
  
### <a name="supported-numeric-and-date-time-ranges"></a>Intervalos numéricos e de data-hora com suporte  
As fórmulas em modelos de tabela na memória estão sujeitas às mesmas limitações do Excel em relação aos valores máximos permitidos para números reais e datas. No entanto, podem surgir diferenças quando o valor máximo é retornado de um cálculo ou consulta ou quando valores são convertidos, arredondados ou truncados.  
  
-   Se valores de tipos **Currency** e **Real** forem multiplicados e o resultado for maior do que o máximo possível, no modo DirectQuery, nenhum erro será gerado e um nulo será retornado.  
  
-   Em modelos na memória, nenhum erro é gerado, mas o valor máximo é retornado.  
  
Em geral, como os intervalos de datas aceitos são diferentes para o Excel e o SQL Server, é possível garantir que os resultados coincidam apenas quando as datas estiverem dentro do intervalo de datas comum, o que inclui as seguintes datas:  
  
-   Data mais antiga: 1º de março de 1990  
  
-   Data mais recente: 31 de dezembro de 9999  
  
Se qualquer data usada em fórmulas ficar fora desse intervalo, a fórmula resultará em um erro ou os resultados não coincidirão.  
  
**Valores de ponto flutuante com suporte de CEILING**  
EXEMPLO: `EVALUATE ROW("x", CEILING(-4.398488E+30, 1))`  
  
O equivalente Transact-SQL da função DAX CEILING somente oferece suporte a valores com magnitude de 10^19 ou menos. Uma regra prática é que os valores de ponto flutuante devem se ajustar em **bigint**.  
  
**Funções Datepart com datas fora do intervalo**  
É garantido que os resultados no modo DirectQuery correspondam àqueles nos modelos na memória somente quando a data usada como argumento está no intervalo de datas válido. Se essas condições não forem atendidas, um erro será gerado ou a fórmula retornará resultados diferentes nos modos DirectQuery e na memória.  
  
EXEMPLO: `MONTH(0)` ou `YEAR(0)`  
  
No modo DirectQuery, as expressões retornam 12 e 1899, respectivamente.  
  
Nos modelos na memória, as expressões retornam 1 e 1900, respectivamente.  
  
EXEMPLO:  `EOMONTH(0.0001, 1)`  
  
Os resultados dessa expressão somente coincidirão quando os dados fornecidos como um parâmetro estiverem dentro do intervalo de datas válido.  
  
EXEMPLO: `EOMONTH(blank(), blank())` ou `EDATE(blank(), blank())`  
  
Os resultados dessa expressão devem ser iguais no modo DirectQuery e no modo na memória.  
  
**Truncamento de valores temporais**  
EXEMPLO: `SECOND(1231.04097222222)`  
  
No modo DirectQuery, o resultado é truncado, de acordo com as regras do SQL Server, e a expressão é avaliada como 59.  
  
Em modelos na memória, os resultados de cada operação provisória são arredondados; portanto, a expressão é avaliada como 0.  
  
O seguinte exemplo demonstra como esse valor é calculado:  
  
1.  A fração da entrada (0,04097222222) é multiplicada por 24.  
  
2.  O valor de hora resultante (0,98333333328) é multiplicado por 60.  
  
3.  O valor de minuto resultante é 58,9999999968.  
  
4.  A fração do valor de minuto (0,9999999968) é multiplicada por 60.  
  
5.  O segundo valor resultante (59,999999808) é arredondado para 60.  
  
6.  60 é equivalente a 0.  
  
**Não há suporte para o tipo de dados SQL Time**  
Modelos na memória não dão suporte ao uso do novo tipo de dados SQL **Time** . No modo DirectQuery, fórmulas que referenciam colunas com esse tipo de dados retornarão um erro. Colunas de dados temporais não podem ser importadas para um modelo na memória.  
  
No entanto, às vezes o mecanismo converte o valor temporal em um tipo de dados aceitável e a fórmula retorna um resultado.  
  
Esse comportamento afeta todas as funções que usam uma coluna de data como um parâmetro.  
  
### <a name="bkmk_Currency"></a>Currency  
No modo DirectQuery, se o resultado de uma operação aritmética tiver o tipo **Currency**, o valor deverá estar dentro do seguinte intervalo:  
  
-   Mínimo: -922337203685477,5808  
  
-   Máximo: 922337203685477,5807  
  
**Combinação dos tipos de dados currency e REAL**  
EXEMPLO: `Currency sample 1`  
  
Se os tipos **Currency** e **Real** forem multiplicados e o resultado for maior que 9223372036854774784 (0x7ffffffffffffc00), o modo DirectQuery não gerará um erro.  
  
Em um modelo na memória, um erro será gerado se o valor absoluto do resultado for maior que 922337203685477,4784.  
  
**A operação resulta em um valor fora do intervalo**  
EXEMPLO: `Currency sample 2`  
  
Se as operações em quaisquer dois valores de moeda resultarem em um valor que esteja fora do intervalo especificado, um erro será gerado em modelos na memória, mas não em modelos DirectQuery.  
  
**Combinação de currency com outros tipos de dados**  
A divisão dos valores de moeda por valores de outros tipos numeric pode apresentar resultados diferentes.  
  
### <a name="bkmk_Aggregations"></a>Funções de agregação  
As funções estatísticas em uma tabela com uma linha retornam resultados diferentes. As funções de agregação em tabelas vazias também se comportam de modo diferente em modelos na memória e no modo DirectQuery.  
  
**Funções estatísticas em uma tabela com uma única linha**  
Se a tabela usada como argumento contiver uma única linha, no modo DirectQuery, as funções estatísticas, como STDEV e VARx, retornarão nulo.  
  
Em um modelo na memória, uma fórmula que usa STDEV ou VARx em uma tabela com uma única linha retorna um erro de divisão por zero.  
  
### <a name="bkmk_Text"></a>Funções de texto  
Como os repositórios de dados relacionais fornecem tipos de dados de texto diferentes dos do Excel, talvez você veja resultados diferentes ao pesquisar cadeias de caracteres ou trabalhar com subcadeias. O comprimento das cadeias de caracteres também pode ser diferente.  
  
Em geral, qualquer função de manipulação de cadeia de caracteres que use colunas de tamanho fixo como argumentos pode ter resultados diferentes.  
  
Além disso, no SQL Server, algumas funções de texto oferecem suporte para argumentos adicionais que não são fornecidos no Excel. Se a fórmula exigir o argumento ausente, você poderá obter resultados diferentes ou erros no modelo na memória.  
  
**Operações que retornam um caractere usando LEFT, RIGHT etc. podem retornar o caractere correto, mas com o uso de maiúsculas/minúsculas diferente, ou nenhum resultado**  
EXEMPLO: `LEFT([“text”], 2)`  
  
No modo DirectQuery, o uso de maiúsculas/minúsculas do caractere retornado sempre é exatamente igual ao da letra armazenada no banco de dados. No entanto, o mecanismo xVelocity usa um algoritmo diferente para compactação e indexação de valores, para melhorar o desempenho.  
  
Por padrão, é usado o agrupamento Latin1_General, que não diferencia maiúsculas/minúsculas, mas diferencia acentos. Portanto, se houver várias instâncias de uma cadeia de caracteres de texto em minúsculas, maiúsculas ou minúsculas/maiúsculas, todas as instâncias serão consideradas a mesma cadeia de caracteres e somente a primeira instância da cadeia de caracteres será armazenada no índice. Todas as funções de texto que operam em cadeias de caracteres armazenadas recuperarão a parte especificada do formulário indexado. Assim, a fórmula de exemplo retornaria o mesmo valor de toda a coluna, usando a primeira instância como a entrada.  
  
Esse comportamento também se aplica a outras funções de texto, incluindo RIGHT, MID etc.  
  
**O comprimento da cadeia de caracteres afeta os resultados**  
EXEMPLO: `SEARCH(“within string”, “sample target  text”, 1, 1)`  
  
Se você procurar uma cadeia de caracteres usando a função SEARCH, e a cadeia de caracteres de destino for maior do que a cadeia de caracteres interna, o modo DirectQuery gerará um erro.  
  
Em um modelo na memória, a cadeia de caracteres pesquisada é retornada, mas com seu comprimento truncado para o comprimento do &lt;texto interno&gt;.  
  
EXEMPLO: `EVALUATE ROW("X", REPLACE("CA", 3, 2, "California") )`  
  
Se o comprimento da cadeia de caracteres de substituição for maior que o comprimento da cadeia de caracteres original, no modo DirectQuery, a fórmula retornará nulo.  
  
Em modelos na memória, a fórmula seguirá o comportamento do Excel, que concatena a cadeia de caracteres de origem e a cadeia de caracteres de substituição, que retorna CACalifornia.  
  
**TRIM implícito no meio das cadeias de caracteres**  
EXEMPLO: `TRIM(“ A sample sentence with leading white space”)`  
  
O modo DirectQuery traduz a função DAX TRIM na instrução SQL `LTRIM(RTRIM(<column>))`. Assim, somente os espaços em branco à esquerda e à direita são removidos.  
  
Em contrapartida, a mesma fórmula em um modelo na memória remove espaços na cadeia de caracteres, de acordo com o comportamento do Excel.  
  
**RTRIM implícito com o uso da função LEN**  
EXEMPLO: `LEN(‘string_column’)`  
  
Como o SQL Server, o modo DirectQuery remove automaticamente o espaço em branco da extremidade das colunas de cadeia de caracteres: ou seja, ele executa um RTRIM implícito. Assim, as fórmulas que usam a função LEN poderão retornar valores diferentes se a cadeia de caracteres tiver espaços à direita.  
  
**O modo Na Memória tem suporte para parâmetros adicionais para SUBSTITUTE**  
EXEMPLO: `SUBSTITUTE([Title],”Doctor”,”Dr.”)`  
  
EXEMPLO: `SUBSTITUTE([Title],”Doctor”,”Dr.”, 2)`  
  
No modo DirectQuery, você pode usar apenas a versão dessa função que tem três (3) parâmetros: uma referência a uma coluna, o texto antigo e o novo texto. Se você usar a segunda fórmula, um erro será gerado.  
  
Em modelos na memória, você pode usar um quarto parâmetro opcional para especificar o número da instância da cadeia de caracteres a ser substituída. Por exemplo, você pode substituir apenas a segunda instância etc.  
  
**Restrições em comprimentos de cadeia de caracteres para operações REPT**  
Em modelos na memória, o comprimento de uma cadeia de caracteres resultante de uma operação usando REPT deve ser inferior a 32.767 caracteres.  
  
Essa limitação não se aplica no modo DirectQuery.  
  
**As operações de subcadeia retornam resultados diferentes, dependendo do tipo de caractere**  
EXEMPLO: `MID([col], 2, 5)`  
  
Se o texto de entrada for **varchar** ou **nvarchar**, o resultado da fórmula sempre será o mesmo.  
  
No entanto, se o texto for um caractere de comprimento fixo e o valor de *&lt;num_char&gt;* for maior que o comprimento da cadeia de caracteres de destino, no modo DirectQuery, um espaço em branco será adicionado ao fim da cadeia de caracteres resultante.  
  
Em um modelo na memória, o resultado termina no último caractere da cadeia de caracteres, sem preenchimento.  


## <a name="see-also"></a>Consulte também  
[Modo DirectQuery (SSAS tabular)](http://msdn.microsoft.com/en-us/45ad2965-05ec-4fb1-a164-d8060b562ea5)  
  



