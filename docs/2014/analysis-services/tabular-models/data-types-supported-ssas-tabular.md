---
title: Tipos de dados com suporte (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 92993f7b-7243-4aec-906d-0b0379798242
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2502b65b1b13f8ed819c138fdfe429390a905a56
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939754"
---
# <a name="data-types-supported-ssas-tabular"></a>Tipos de dados com suporte (SSAS tabular)
  Este artigo descreve os tipos de dados que podem ser usados em modelos tabulares e discute a conversão implícita de tipos de dados quando dados são calculados ou usados em uma fórmula DAX (Data Analysis Expressions).  
  
 Este artigo inclui as seções a seguir:  
  
-   [Tipos de dados usados em modelos tabulares](#bkmk_data_types)  
  
-   [Conversão de tipo de dados implícita e explícita em fórmulas DAX](#bkmk_implicit)  
  
-   [Manipulação de espaços em branco, cadeias de caracteres vazias e valores zero](#bkmk_hand_blanks)  
  
##  <a name="data-types-used-in-tabular-models"></a><a name="bkmk_data_types"></a>Tipos de dados usados em modelos de tabela  
 Há suporte para os seguintes tipos de dados. Quando você importa dados ou usa um valor em uma fórmula, mesmo quando a fonte de dados original contém um tipo de dados diferente, os dados serão convertidos em um dos tipos de dados a seguir. Valores que resultam de fórmulas também usam esses tipos de dados.  
  
 Em geral, esses tipos de dados são implementados para permitir cálculos precisos em colunas calculadas e, para consistência, as mesmas restrições se aplicam ao resto dos dados no modelo.  
  
 Os formatos usados para números, moeda, datas e horas devem seguir o formato da localidade especificada no cliente usado para trabalhar com dados de modelo. É possível usar as opções de formatação do modelo para controlar a forma como o valor é exibido.  
  
||||  
|-|-|-|  
|Tipo de dados em modelo|Tipos de dados em DAX|Descrição|  
|Número Inteiro|Um valor inteiro de 64 bits (oito bytes) <sup>1, 2</sup>|Números sem casas decimais. Inteiros podem ser números positivos ou negativos, mas devem ser números inteiros entre -9.223.372.036.854.775.808 (-2^63) e 9.223.372.036.854.775.807 (2^63-1).|  
|Número Decimal|Um número real de 64 bits (oito bytes) <sup>1, 2</sup>|Números reais são números que podem ter casas decimais. Os números reais abrangem uma grande variedade de valores:<br /><br /> Valores negativos de -1,79E +308 a -2,23E -308<br /><br /> Zero<br /><br /> Valores positivos de 2,23E -308 a 1,79E + 308<br /><br /> No entanto, o número de dígitos significativos está limitado a 17 dígitos decimais.|  
|Booliano|Booliano|Um valor True ou False.|  
|Texto|String|Uma cadeia de caracteres de dados de caractere Unicode. Podem ser cadeias de caracteres, números ou datas representados em um formato de texto.|  
|Data|Date/time|Datas e horas em uma representação de data-hora aceita.<br /><br /> As datas válidas são todas as datas depois de 1º de março de 1900.|  
|Moeda|Moeda|O tipo de dados de moeda permite valores entre -922.337.203.685.477,5808 e 922.337.203.685.477,5807 com quatro dígitos decimais de precisão fixa.|  
|N/D|Em Branco|Um espaço em branco é um tipo de dados no DAX que representa e substitui nulos SQL. É possível criar um espaço em branco usando a função BLANK e testar se há espaços em branco usando a função lógica, ISBLANK.|  
  
 <sup>1</sup> as fórmulas DAX não dão suporte a tipos de dados menores que os listados na tabela.  
  
 <sup>2</sup> se você tentar importar dados com valores numéricos muito grandes, a importação poderá falhar com o seguinte erro:  
  
 Erro de banco de dados na memória: a \<column name> coluna ' ' da \<table name> tabela ' ' contém um valor, ' 7976931348623157e e + 308 ', que não tem suporte. A operação foi cancelada.  
  
 Esse erro ocorre porque o designer de modelos usa esse valor para representar nulos. Os valores na lista a seguir são sinônimos do valor nulo mencionado anterior:  
  
||  
|-|  
|Valor|  
|9223372036854775807|  
|-9223372036854775808|  
|1,7976931348623158e+308|  
|2,2250738585072014e-308|  
  
 Você deve remover o valor dos dados e tentar importá-los novamente.  
  
> [!NOTE]  
>  Você não pode importar de uma coluna de **varchar(max)** que contém um comprimento da cadeia de caracteres de mais de 131.072 caracteres.  
  
### <a name="table-data-type"></a>Tipo de dados de tabela  
 Além disso, a DAX usa um tipo de dados *table* . Esse tipo de dados é usado pela DAX em muitas funções, como agregações e cálculos de inteligência de hora. Algumas funções exigem uma referência a uma tabela; outras funções retornam uma tabela que pode ser usada como entrada para outras funções. Em algumas funções que exigem uma tabela como entrada, você pode especificar uma expressão que é avaliada como uma tabela; para algumas funções, é necessária uma referência a uma tabela base. Para obter informações sobre os requisitos de funções específicas, consulte [Referência de função DAX](/dax/dax-function-reference).  
  
##  <a name="implicit-and-explicit-data-type-conversion-in-dax-formulas"></a><a name="bkmk_implicit"></a>Conversão de tipo de dados implícita e explícita em fórmulas DAX  
 Cada função DAX tem requisitos específicos quanto aos tipos de dados que são usados como entradas e saídas. Por exemplo, algumas funções exigem inteiros para alguns argumentos e datas para outros; outras funções exigem texto ou tabelas.  
  
 Se os dados na coluna especificada como um argumento forem incompatíveis com o tipo de dados exigido pela função, em muitos casos DAX retornará um erro. No entanto, sempre que possível, o DAX tentará converter implicitamente os dados para o tipo de dados necessário. Por exemplo:  
  
-   Você pode digitar um número, por exemplo "123", como uma cadeia de caracteres. O DAX analisará a cadeia de caracteres e tentará especificá-la como um tipo de dados numérico.  
  
-   Você pode adicionar TRUE + 1 e obter o resultado 2, pois TRUE é implicitamente convertido para o número 1 e a operação 1+1 é executada.  
  
-   Se você adicionar valores em duas colunas e um valor for representado como texto ("12") e o outro como um número (12), o DAX converte implicitamente a cadeia de caracteres em um número e, em seguida, faz a adição para chegar a um resultado numérico. A seguinte expressão retorna 44: = "22" + 22  
  
-   Se você tentar concatenar dois números, o suplemento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vai apresentá-los como cadeias de caracteres e, em seguida, concatená-los. A seguinte expressão retorna "1234": = 12 & 34  
  
 A tabela a seguir resume as conversões implícitas de tipo de dados executadas em fórmulas. Em geral, o designer de modelos semânticos se comporta como o Microsoft Excel e executa conversões implícitas sempre que possível quando exigido pela operação especificada.  
  
### <a name="table-of-implicit-data-conversions"></a>Tabela de conversões implícitas de dados  
 O tipo de conversão executada é determinado pelo operador, que transmite os valores que ele requer antes de executar a operação solicitada. Essas tabelas listam os operadores e indicam a conversão que é realizada em cada tipo de dados na coluna quando ele é emparelhado com o tipo de dados na linha que intersecciona essa coluna.  
  
> [!NOTE]  
>  Tipos de dados de texto não são incluídos nessas tabelas. Quando um número é representado como em um formato de texto, em alguns casos, o designer de modelos tentará determinar o tipo de número e representá-lo como um número.  
  
#### <a name="addition-"></a>Adição (+)  
  
||||||  
|-|-|-|-|-|  
|Operador (+)|INTEGER|CURRENCY|REAL|Date/time|  
|INTEGER|INTEGER|CURRENCY|REAL|Date/time|  
|CURRENCY|CURRENCY|CURRENCY|REAL|Date/time|  
|REAL|REAL|REAL|REAL|Date/time|  
|Date/time|Date/time|Date/time|Date/time|Date/time|  
  
 Por exemplo, se um número real é usado em uma operação de adição em combinação com dados de moedas, os dois valores são convertidos em REAL e o resultado é retornado como REAL.  
  
#### <a name="subtraction--"></a>Subtração (-)  
 Na tabela a seguir, o cabeçalho da linha é o minuendo (lado esquerdo) e o cabeçalho da coluna é o subtraendo (lado direito).  
  
||||||  
|-|-|-|-|-|  
|Operador (-)|INTEGER|CURRENCY|REAL|Date/time|  
|INTEGER|INTEGER|CURRENCY|REAL|REAL|  
|CURRENCY|CURRENCY|CURRENCY|REAL|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|Date/time|Date/time|Date/time|Date/time|Date/time|  
  
 Por exemplo, se uma data é usada em uma operação de subtração com qualquer outro tipo de dados, ambos os valores são convertidos em datas e o valor retornado também é uma data.  
  
> [!NOTE]  
>  Os modelos tabulares também dão suporte ao operador unário, - (negativo), mas esse operador não altera o tipo de dados do operando.  
  
#### <a name="multiplication-"></a>Multiplicação (*)  
  
||||||  
|-|-|-|-|-|  
|Operador (*)|INTEGER|CURRENCY|REAL|Date/time|  
|INTEGER|INTEGER|CURRENCY|REAL|INTEGER|  
|CURRENCY|CURRENCY|REAL|CURRENCY|CURRENCY|  
|REAL|REAL|CURRENCY|REAL|REAL|  
  
 Por exemplo, se um inteiro for combinado com um número real em uma operação de multiplicação, os dois números são convertidos em números reais, e o valor retornado também é REAL.  
  
#### <a name="division-"></a>Divisão (/)  
 Na tabela a seguir, o cabeçalho da linha é o numerador e o cabeçalho da coluna é o denominador.  
  
||||||  
|-|-|-|-|-|  
|Operador (/)<br /><br /> (Linha/coluna)|INTEGER|CURRENCY|REAL|Date/time|  
|INTEGER|REAL|CURRENCY|REAL|REAL|  
|CURRENCY|CURRENCY|REAL|CURRENCY|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|Date/time|REAL|REAL|REAL|REAL|  
  
 Por exemplo, se um inteiro for combinado com um valor de moeda em uma operação de divisão, os dois valores são convertidos em números reais e o resultado também é um número real.  
  
#### <a name="comparison-operators"></a>Operadores de comparação  
 Em expressões de comparação, os valores Boolianos são considerados maiores que os valores da cadeia de caracteres, que são considerados maiores que os valores numéricos ou de data/hora; os números e os valores de data/hora são considerados da mesma classificação. Nenhuma conversão implícita é executada para valores de cadeia de caracteres ou Boolianos; BLANK ou um valor em branco é convertido em 0/""/false, dependendo do tipo de dados do outro valor comparado.  
  
 As seguintes expressões DAX ilustram esse comportamento:  
  
 `=IF(FALSE()>"true","Expression is true", "Expression is false")` retorna `"Expression is true"`  
  
 `=IF("12">12,"Expression is true", "Expression is false")` retorna `"Expression is true"`  
  
 `=IF("12"=12,"Expression is true", "Expression is false")` retorna `"Expression is false"`  
  
 As conversões são executadas implicitamente para tipos numéricos ou de data/hora, conforme descrito na tabela a seguir:  
  
||||||  
|-|-|-|-|-|  
|Operador de Comparação|INTEGER|CURRENCY|REAL|Date/time|  
|INTEGER|INTEGER|CURRENCY|REAL|REAL|  
|CURRENCY|CURRENCY|CURRENCY|REAL|REAL|  
|REAL|REAL|REAL|REAL|REAL|  
|Date/time|REAL|REAL|REAL|Date/time|  
  
##  <a name="handling-of-blanks-empty-strings-and-zero-values"></a><a name="bkmk_hand_blanks"></a>Manipulação de espaços em branco, cadeias de caracteres vazias e valores zero  
 A maneira como o DAX manipula valores zero, nulos e cadeias de caracteres vazias é diferente do Microsoft Excel e do SQL Server. Esta seção descreve as diferenças e descreve como estes tipos de dados são tratados.  
  
 É importante lembrar-se de que um valor em branco, uma célula vazia ou um valor ausente são todos representados pelo mesmo novo tipo de valor, um BLANK. A forma como espaços em branco são tratados em operações, como adição ou concatenação, depende de cada função. Você também pode gerar elementos em branco usando a função BLANK, ou testar elementos em branco usando a função ISBLANK. Nulos de banco de dados não têm suporte dentro de um modelo semântico, e nulos são implicitamente convertidos em espaços em branco quando uma coluna que contém um valor nulo é referenciada em uma fórmula DAX.  
  
### <a name="defining-blanks-nulls-and-empty-strings"></a>Definindo espaços em branco, nulos e cadeias de caracteres vazias  
 A tabela a seguir resume as diferenças entre DAX e o Microsoft Excel, com relação ao modo como espaços em branco são tratados.  
  
||||  
|-|-|-|  
|Expression|DAX|Excel|  
|BLANK + BLANK|BLANK|0 (zero)|  
|BLANK +5|5|5|  
|BLANK * 5|BLANK|0 (zero)|  
|5/BLANK|Infinity|Erro|  
|0/BLANK|NaN|Error|  
|BLANK/BLANK|BLANK|Erro|  
|FALSE OR BLANK|FALSO|FALSE|  
|FALSE AND BLANK|FALSO|FALSE|  
|TRUE OR BLANK|VERDADEIRO|TRUE|  
|TRUE AND BLANK|FALSO|VERDADEIRO|  
|BLANK OR BLANK|BLANK|Erro|  
|BLANK AND BLANK|BLANK|Erro|  
  
 Para obter detalhes sobre como uma determinada função ou operador manipula espaços em branco, consulte os tópicos individuais de cada função DAX, na seção, [Referência de função DAX](/dax/dax-function-reference).  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes de dados &#40;SSAS de tabela&#41;](../data-sources-ssas-tabular.md)   
 [Importar dados &#40;SSAS de Tabela&#41;](../import-data-ssas-tabular.md)  
  
  
