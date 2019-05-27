---
title: Conteúdo de FORMAT_STRING (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- formats [Analysis Services], string values
- VALUE property
- formats [Analysis Services], numeric values
- FORMATTED_VALUE property
- FORMAT_STRING contents
ms.assetid: c354c938-0328-4b8e-adc5-3b52fd2a7152
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b80cfeae2957753cfe96d54dcbe0052e19db741
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66074472"
---
# <a name="formatstring-contents-mdx"></a>Conteúdo de FORMAT_STRING (MDX)
  A propriedade de célula `FORMAT_STRING` formata a propriedade de célula `VALUE`, criando o valor da propriedade de célula `FORMATTED_VALUE`. A propriedade de célula `FORMAT_STRING` lida com valores numéricos e cadeias de caracteres, aplicando a expressão de formato ao valor para retornar um valor formatado para a propriedade de célula `FORMATTED_VALUE`. As tabelas a seguir detalham a sintaxe e os caracteres de formatação usados para lidar com valores de cadeia de caracteres e numéricos.  
  
## <a name="string-values"></a>Valores de cadeia de caracteres  
 Uma expressão de formato para cadeias de caracteres pode ter uma seção ou duas seções separadas por ponto-e-vírgula (;).  
  
|Uso|Resultado|  
|-----------|------------|  
|Uma seção|O formato é aplicado a todos os valores da cadeia de caracteres.|  
|Duas seções|A primeira seção é aplicada aos dados da cadeia de caracteres, enquanto a segunda é aplicada a valores nulos de comprimento zero ("").|  
  
 Os caracteres descritos na tabela a seguir podem aparecer na cadeia de caracteres de formato das cadeias de caracteres.  
  
|Caractere|Descrição|  
|---------------|-----------------|  
|@|Representa um espaço reservado de caractere que exibe um caractere ou um espaço. Se a cadeia de caracteres tiver um caractere na posição onde aparece um sinal arroba (@) na cadeia de caracteres de formato, a cadeia de caracteres formatada exibirá o caractere. Caso contrário, a cadeia de caracteres formatada exibirá um espaço naquela posição. Os espaços reservados são preenchidos da direita para a esquerda, a menos que haja um ponto de exclamação (!) na cadeia de caracteres de formato.|  
|&|Representa um espaço reservado de caractere que exibe um caractere ou nada. Se a cadeia de caracteres tiver um caractere na posição onde aparece um sinal E comercial (&), a cadeia de caracteres formatada exibirá o caractere. Caso contrário, a cadeia de caracteres formatada não exibirá nada. Os espaços reservados são preenchidos da direita para a esquerda, a menos que haja um ponto de exclamação (!) na cadeia de caracteres de formato.|  
|\<|Força o uso de letra minúscula. A cadeia de caracteres formatada exibe todos os caracteres em formato de letra minúscula.|  
|>|Força o uso de letra maiúscula. A cadeia de caracteres formatada exibe todos os caracteres em formato de letra maiúscula.|  
|!|Força o preenchimento da esquerda para a direita de espaços reservados. (O padrão de preenchimento de espaços reservados é da direita para a esquerda.)|  
  
## <a name="numeric-values"></a>Valores numéricos  
 Uma expressão de formato definida pelo usuário para números pode ter, em qualquer lugar, de uma a quatro seções separadas por ponto-e-vírgula. Se o argumento de formato contiver um dos formatos numéricos nomeados, apenas uma seção será permitida.  
  
|Uso|Resultado|  
|-----------|------------|  
|Uma seção|A expressão de formato é aplicada a todos os valores.|  
|Duas seções|A primeira seção é aplicada a valores positivos e zeros; a segunda a valores negativos.|  
|Três seções|A primeira seção é aplicada a valores positivos, a segunda a valores negativos e a terceira a zeros.|  
|Quatro seções|A primeira seção é aplicada a valores positivos, a segunda a valores negativos, a terceira a zeros e a quarta a valores nulos.|  
  
 O exemplo a seguir possui duas seções. A primeira define o formato dos valores positivos e dos zeros, enquanto a segunda define o formato dos valores negativos.  
  
```  
"$#,##0;($#,##0)"  
```  
  
 Se você incluir ponto-e-vírgula sem colocar nada entre eles, a seção perdida será impressa usando o formato do valor positivo. Por exemplo, o formato a seguir exibe valores positivos e negativos usando o formato da primeira seção e exibe "Zero" se o valor for zero:  
  
```  
"$#,##0;;\Z\e\r\o"  
```  
  
 A tabela a seguir identifica os caracteres que podem aparecer na cadeia de caracteres de formato para formatos numéricos.  
  
|Caractere|Descrição|  
|---------------|-----------------|  
|None|Exibe o número sem qualquer formatação.|  
|**0**|Representa um espaço reservado de dígito que exibe um dígito ou um zero (0).<br /><br /> Se o número tiver um dígito na posição onde aparece um zero na cadeia de caracteres de formato, o valor formatado exibirá o dígito. Caso contrário, o valor formatado exibirá um zero nessa posição.<br /><br /> Se o número tiver menos dígitos que zeros (em qualquer lado da divisão decimal) na cadeia de caracteres de formato, o valor formatado exibirá zeros à esquerda e à direita.<br /><br /> Se o número tiver mais dígitos à direita do separador decimal que zeros à direita do separador decimal na expressão de formato, o valor formatado arredondará o número para o mesmo número de casas decimais que a quantidade de zeros.<br /><br /> Se o número tiver mais dígitos à esquerda do separador decimal que zeros à esquerda do separador decimal na expressão de formato, o valor formatado exibirá os dígitos adicionais sem alteração.|  
|**#**|Representa um espaço reservado de dígito que exibe um dígito ou nada.<br /><br /> Se a expressão tiver um dígito na posição em que aparece um sinal numérico (**#**) na cadeia de caracteres de formato, o valor formatado exibirá o dígito. Caso contrário, o valor formatado não exibirá nada naquela posição.<br /><br /> O espaço reservado para sinal numérico (**#**) funciona como o espaço reservado para o dígito zero (**0**), exceto pelo fato de que os zeros à esquerda e à direita não serão exibidos se o número tiver a mesma quantidade de dígitos, ou menos, que de caracteres **#** em qualquer um dos lados do separador decimal na expressão de formato.|  
|**.**|Representa um espaço reservado decimal que determina quantos dígitos serão exibidos à esquerda e à direita do separador decimal.<br /><br /> Se a expressão de formato contiver apenas caracteres de sinal numérico (**#**) à esquerda do ponto (**.**), números menores que 1 começaram com um separador decimal. Para exibir um zero à esquerda no caso de números fracionais, use zero (0) como o primeiro espaço reservado para dígito à esquerda do separador decimal.<br /><br /> O caractere real usado como espaço reservado decimal na saída formatada depende do formato numérico reconhecido pelo sistema do computador.<br /><br /> Observação: Em algumas localidades, uma vírgula é usada como separador decimal.|  
|**%**|Representa um espaço reservado de porcentagem. A expressão é multiplicada por 100. O caractere por cento (**%**) é inserido na posição em que o percentual aparece na cadeia de caracteres de formato.|  
|**,**|Representa um separador de milhar que separa os milhares das centenas em um número com quatro ou mais casas à esquerda do separador decimal.<br /><br /> O uso padrão do separador de milhar será especificado se o formato contiver um separador de milhar encerrado em espaços reservados para dígitos (**0** ou **#**).<br /><br /> Dois separadores de milhar adjacentes, ou um separador de milhar imediatamente à esquerda do separador decimal (independentemente de um decimal ter sido especificado), significa "escalar o número dividindo-o por 1000, arredondando se necessário". Por exemplo, você pode usar a cadeia de caracteres de formato "**##0**", para representar 100 milhões como 100. Números menores que 1 milhão são exibido como 0. Dois separadores de milhar adjacentes em uma posição que não seja imediatamente à esquerda do separador decimal são tratados como se estivessem especificando o uso de um separador de milhar.<br /><br /> O caractere real usado como separador de milhar na saída formatada depende do formato numérico reconhecido pelo sistema do computador.<br /><br /> Observação: Em algumas localidades, um ponto é usado como separador de milhar.|  
|**:**|Representa um separador de tempo que separa horas, minutos e segundos quando são formatados valores de tempo.<br /><br /> Observação: Em algumas localidades, outros caracteres podem ser usados como o separador de hora.<br /><br /> O caractere real usado como separador de tempo na saída formatada é determinado pelas configurações do sistema do computador.|  
|**/**|Representa um separador de data que separa dia, mês e ano quando são formatados valores de data.<br /><br /> O caractere real usado como separador de data na saída formatada é determinado pelas configurações do sistema do computador.<br /><br /> Observação: Em algumas localidades, outros caracteres podem ser usados como o separador de data.|  
|**E - E+ e - e+**|Representa formato científico.<br /><br /> Se a expressão de formato contiver pelo menos um espaço reservado para dígito (**0** ou **#**) à direita de **E-**, **E+**, **e-** ou **e+**, o valor formatado será exibo em formato científico e E ou e será inserido entre o número e seu exponente. O número de espaços reservados para dígito determina o número de dígitos do exponente. Use **E-** ou **e-** para incluir um sinal de menos junto a exponentes negativos. Use **E+** ou **e+** para incluir um sinal de menos junto a exponentes negativos e um sinal de mais junto a exponentes positivos.|  
|**- + $ ( )**|Exibe um caractere literal.<br /><br /> Para exibir um outro caractere que não seja um dos listados, coloque uma barra invertida (**\\**) antes do caractere ou coloque-o entre aspas duplas (**" "**).|  
|**\\**|Exibe o próximo caractere da cadeia de caracteres de formato.<br /><br /> Para exibir um caractere que tem um significado especial como um caractere literal, coloque uma barra invertida (**\\**) antes dele. A barra invertida não é exibida. Usar uma barra invertida é o mesmo que colocar o próximo caractere entre aspas duplas. Para exibir uma barra invertida, use duas barras invertidas (**\\\\**). Estes são exemplos de caracteres que não podem ser exibidos como caracteres literais:<br /><br /> Os caracteres de formatação de data e a formatação de hora -**uma**, **c**, **1!d**, **h**, **m**, **n**, **p**, **p**, **s**, **t**, **w**, **y** , **/**, e **:**<br /><br /> A formatação numérica caracteres -**#**, **0**, **%**, **eletrônico**, **e**, **vírgula**, e **período**<br /><br /> A formatação de cadeia de caracteres -**@**, **&**, **\<**, **>**, e **!**|  
|**"ABC"**|Exibe a cadeia de caracteres entre aspas duplas (**" "**).<br /><br /> Para incluir uma cadeia de caracteres em formato de um código, use Chr (**34**) para incluir o texto. (O código de caractere para aspas duplas é **34**.)|  
  
### <a name="named-numeric-formats"></a>Formatos numéricos nomeados  
 A tabela a seguir identifica os nomes de formatos numéricos predefinidos:  
  
|Nome do formato|Descrição|  
|-----------------|-----------------|  
|`General Number`|Exibe o número sem nenhum separador de milhar.|  
|`Currency`|Exibe o número com um separador de milhar, se apropriado. Exibe dois dígitos à direita do separador decimal. A saída é baseada nas configurações de localidade do sistema.|  
|`Fixed`|Exibe pelo menos um dígito à esquerda e dois dígitos à direita do separador decimal.|  
|`Standard`|Exibe o número com separador de milhar, pelo menos um dígito à esquerda e dois dígitos à direita do separador decimal.|  
|`Percent`|Exibe o número multiplicado por 100 com um sinal de porcentagem (%) à direita. Sempre exibe dois dígitos à direita do separador decimal.|  
|`Scientific`|Usa notação científica padrão.|  
|`Yes/No`|Exibe Não se o número for 0; caso contrário, exibe Sim.|  
|`True/False`|Exibe Falso se o número for 0; caso contrário, exibe Verdadeiro.|  
|`On/Off`|Exibe Desabilitado se o número for 0; caso contrário, exibe Habilitado.|  
  
## <a name="date-values"></a>Valores de data  
 A tabela a seguir identifica os caracteres que podem aparecer na cadeia de caracteres de formatos de data/hora.  
  
|Caractere|Descrição|  
|---------------|-----------------|  
|**:**|Representa um separador de tempo que separa horas, minutos e segundos quando são formatados valores de tempo.<br /><br /> O caractere real usado como separador de tempo na saída formatada é determinado pelas configurações do sistema do computador.<br /><br /> Observação: Em algumas localidades, outros caracteres podem ser usados como o separador de hora.|  
|**/**|Representa um separador de data que separa dia, mês e ano quando são formatados valores de data.<br /><br /> O caractere real usado como separador de data na saída formatada é determinado pelas configurações do sistema do computador.<br /><br /> Observação: Em algumas localidades, outros caracteres podem ser usados para representar o separador de data|  
|**C**|Exibe a data como **ddddd** e a hora como **ttttt**, nessa ordem.<br /><br /> Exibe as informações da data somente se não houver nenhuma parte fracionária no número de série de data. Exibe as informações da data somente se não houver nenhuma parte com número inteiro.|  
|**d**|Exibe o dia como um número sem um zero à esquerda (1-31).|  
|**dd**|Exibe o dia como um número com um zero à esquerda (01 a 31).|  
|**ddd**|Exibe o dia como uma abreviação (DOM-sáb).|  
|**dddd**|Exibe o dia como um nome completo (domingo-sábado).|  
|**ddddd**|Exibe a data completa (incluindo dia, mês e ano), formatada de acordo com a configuração de formato de data abreviada do seu sistema.<br /><br /> No Microsoft Windows, o formato de data abreviada padrão é **d/m/aa**.|  
|**dddddd**|Exibe o número sequencial de data (incluindo dia, mês e ano), formatado de acordo com a configuração de formato de data por extenso reconhecida pelo sistema do computador.<br /><br /> No Windows, o formato de data por extenso padrão é **mmm dd, yyyy**.|  
|**w**|Exibe o dia da semana como um número (de 1 para domingo a 7 para sábado).|  
|**ww**|Exibe a semana do ano como um número (1-54).|  
|**m**|Exibe o mês como um número sem um zero à esquerda (1 a 12).<br /><br /> Se **m** vier imediatamente após **h** ou **hh**, será exibido o minuto em vez do mês.|  
|**mm**|Exibe o mês como um número com um zero à esquerda (01 a 12).<br /><br /> Se **m** vier imediatamente após **h** ou **hh**, será exibido o minuto em vez do mês.|  
|**mmm**|Exibe o mês como uma abreviação (Jan-dez).|  
|**mmmm**|Exibe o mês como um nome completo do mês (janeiro-dezembro).|  
|**q**|Exibe o trimestre do ano como um número (1-4).|  
|**y**|Exibe o dia do ano como um número (1-366).|  
|**yy**|Exibe o ano como um número de dois dígitos (00-99).|  
|**yyyy**|Exibe o ano como um número de quatro dígitos (100-9999).|  
|**h**|Exibe a hora como um número sem zeros à esquerda (0-23).|  
|**hh**|Exibe a hora como um número com zeros à esquerda (00-23).|  
|**n**|Exibe o minuto como um número sem zeros (0 a 59).|  
|**nn**|Exibe o minuto como um número com zeros à esquerda (00-59).|  
|**s**|Exibe o segundo como um número sem zeros (0 a 59).|  
|**ss**|Exibe o segundo como um número com zeros à esquerda (00-59).|  
|**t t t t t**|Exibe a hora como uma hora completa (incluindo hora, minuto e segundo), formatada usando o separador de hora definido pelo formato de tempo por reconhecido pelo sistema do computador.<br /><br /> Um zero à esquerda será exibido se a opção de zero à esquerda estiver selecionada e a hora for anterior a 10:00 no ciclo A.M. ou P.M. ciclo. Por exemplo, 09:59.<br /><br /> No Windows, o formato de hora padrão é **h:mm:ss**.|  
|**AM/PM**|Exibe **AM** em letras maiúsculas com todas as horas entre meia-noite e meio-dia; exibe **PM** em letras maiúsculas com todas as horas entre meio-dia e meia-noite.<br /><br /> Observação: Usa o relógio de 12 horas.|  
|**am/pm**|Exibe **am** em letras minúsculas com todas as horas entre meia-noite e meio-dia; exibe **pm** em letras minúsculas com todas as horas entre meio-dia e meia-noite.<br /><br /> Observação: Usa o relógio de 12 horas.|  
|**A/P**|Exibe **A** em letras maiúsculas com todas as horas entre meia-noite e meio-dia; exibe **P** em letras maiúsculas com todas as horas entre meio-dia e meia-noite.<br /><br /> Observação: Usa o relógio de 12 horas.|  
|**a/p**|Exibe **a** em letras minúsculas com todas as horas entre meia-noite e meio-dia; exibe **p** em letras minúsculas com todas as horas entre meio-dia e meia-noite.<br /><br /> Observação: Usa o relógio de 12 horas.|  
|**AMPM**|Exibe o texto da cadeia de caracteres AM conforme definido pelo sistema do computador com todas as horas entre meia-noite e meio-dia; Exibe o texto da cadeia de caracteres PM conforme definido pelo sistema do computador com todas as horas entre meio-dia e meia-noite.<br /><br /> Observação: Usa o relógio de 12 horas.<br /><br /> **AMPM** pode ser em letras maiúsculas ou minúsculas, mas o formato da cadeia de caracteres exibida corresponde à cadeia de caracteres conforme definida pelas configurações do sistema do computador.<br /><br /> No Windows, o formato padrão é **AM/PM**.|  
  
### <a name="named-date-formats"></a>Formatos de data nomeados  
 A tabela a seguir identifica os nomes de formato de data e hora predefinidos:  
  
|Nome do formato|Descrição|  
|-----------------|-----------------|  
|`General Date`|Exibe uma data e/ou hora. Para números reais, exibe uma data e hora, por exemplo, 4/3/93 05:34 PM. Se não houver nenhuma parte fracionária, exibirá só uma data, por exemplo, 4/3/93. Se não houver nenhuma parte inteira, só exibirá uma hora, por exemplo, 05:34 PM. O formato da exibição de data é determinado pelas configurações de sistema.|  
|`Long Date`|Exibe uma data de acordo com o formato de data por extenso de seu sistema.|  
|`Medium Date`|Exibe uma data usando o formato de data médio apropriado para a versão de idioma do aplicativo de host.|  
|`Short Date`|Exibe uma data usando o formato de data curto de seu sistema.|  
|`Long Time`|Exibe uma hora usando o formato de hora longo de seu sistema; inclui horas, minutos e segundos.|  
|`Medium Time`|Exibe uma hora no formato de 12 horas usando horas e minutos e o designator AM/PM.|  
|`Short Time`|Exibe uma hora usando o formato de 24 horas, por exemplo, 17:45.|  
  
## <a name="see-also"></a>Consulte também  
 [LANGUAGE e FORMAT_STRING em FORMATED_VALUE](mdx-cell-properties-formatted-value-property.md)   
 [Usando propriedades da célula &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)   
 [Criando e usando valores de propriedade &#40;MDX&#41;](../../creating-and-using-property-values-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
