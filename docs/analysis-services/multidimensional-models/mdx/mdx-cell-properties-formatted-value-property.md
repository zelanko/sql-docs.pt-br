---
title: LANGUAGE e FORMAT_STRING em FORMATTED_VALUE | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1ad2038e28afb455dd1ad239a2bf02cab99ed4d9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-cell-properties---formattedvalue-property"></a>Propriedades de célula MDX - propriedade FORMATTED_VALUE
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  A propriedade FORMATTED_VALUE é criada com base nas interações das propriedades VALUE, FORMAT_STRING e LANGUAGE da célula. Este tópico explica como essas propriedades interagem para criar a propriedade FORMATTED_VALUE.  
  
## <a name="value-formatstring-language-properties"></a>Propriedades VALUE, FORMAT_STRING, LANGUAGE  
 A tabela a seguir explica o que são essas propriedades, para ajudá-lo na preparação para o uso combinado delas.  
  
 VALUE  
 O valor não formatado da célula.  
  
 FORMAT_STRING  
 O modelo de formatação a ser aplicado ao valor da célula para gerar a propriedade FORMATTED_VALUE  
  
 LANGUAGE  
 A especificação de localidade a ser aplicada junto com FORMAT_STRING para gerar uma versão localizada de FORMATTED_VALUE  
  
## <a name="formattedvalue-constructed"></a>FORMATTED_VALUE construída  
 A propriedade FORMATTED_VALUE é construída com o uso do valor da propriedade VALUE e a aplicação do modelo de formato especificado na propriedade FORMAT_STRING para esse valor. Além disso, sempre que o valor de formatação for um **literal de formatação nomeado** , a especificação da propriedade LANGUAGE modifica a saída de FORMAT_STRING para seguir o uso do idioma da formatação nomeada. Os literais de formatação nomeada são definidos de modo que possam ser localizados. Por exemplo, `"General Date"` é uma especificação que pode ser localizada, em oposição ao seguinte modelo `"YYYY-MM-DD hh:nn:ss",` , que declara que a data deve ser apresentada conforme o definido pelo modelo, independentemente da especificação de idioma.  
  
 Se houver um conflito entre o modelo FORMAT_STRING e a especificação LANGUAGE, FORMAT_STRING substituirá LANGUAGE. Por exemplo, se FORMAT_STRING="$ #0" e LANGUAGE=1034 (Spain), e VALUE=123.456, D_VALUE="$ 123" em vez de FORMATTED_VALUE="€ 123", o formato esperado estará em Euros, porque o valor do modelo do formato substitui o idioma especificado.  
  
### <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram a saída obtida quando LANGUAGE é usado junto com FORMAT_STRING.  
  
 O primeiro exemplo explica os valores numéricos da formatação; o segundo exemplo explica os valores de data e hora da formatação.  
  
 Para cada exemplo, o código MDX é atribuído.  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Os resultados, transpostos, quando a consulta MDX acima estava sendo executada com o uso de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] em um servidor e cliente com a localidade 1033, da seguinte forma:  
  
|Membro|FORMATTED_VALUE|Explicação|  
|------------|----------------------|-----------------|  
|A|$5.040,00|FORMAT_STRING é definido como `Currency` e LANGUAGE é `1033`, informações herdadas do valor de localidade do sistema|  
|B|€ 5.040,00|FORMAT_STRING é definido como `Currency` (herdado de A) e LANGUAGE é definido explicitamente como `1034` (Spain), daí o sinal de Euro, o separador decimal e de milhar diferente.|  
|C|$ 5.040,00|FORMAT_STRING é definido como `$#,##0.00` , uma substituição para Moeda, de A, e LANGUAGE é definido explicitamente para `1034` (Spain). Como a propriedade FORMAT_STRING define explicitamente o símbolo de moeda como $, FORMATTED_VALUE é apresentado com o sinal $. No entanto, como `.` (ponto) e `,` (vírgula) são espaços reservados para separadores de decimal e de milhar, a especificação de idioma os afeta gerando uma saída localizada para separadores decimal e de milhar.|  
|D|5.04E+03|FORMAT_STRING é definido como `Scientific` e LANGUAGE é definido como `1033`, herdados do valor de localidade do sistema, por isso o `.` (ponto) é o separador decimal.|  
|E|5,04E+03|FORMAT_STRING é definido como `Scientific` e LANGUAGE é definido explicitamente como `1034,` , por isso a `,` (vírgula) é o separador decimal.|  
|F|50,40%|FORMAT_STRING é definido como `Percent` e LANGUAGE é definido como `1033`, herdados do valor de localidade do sistema, por isso o `.` (ponto) é o separador decimal.<br /><br /> Observe que VALUE foi alterado de 5040 para 0.5040|  
|G|50,40%|FORMAT_STRING é definido como `Percent`, herdado de F, e LANGUAGE é definido explicitamente como `1034` , por isso a `,` (vírgula) é o separador decimal.<br /><br /> Observe que VALUE foi herdado do valor F.|  
|H|Não|FORMAT_STRING é definido como `YES/NO`, VALUE é definido como 0 e LANGUAGE é definido explicitamente como `1034`; como não há nenhuma diferença entre English NO e Spanish NO, o usuário não vê diferença em FORMATTED_VALUE.|  
|I|SI|FORMAT_STRING é definido como `YES/NO`, VALUE é definido como 59 e LANGUAGE é definido explicitamente como `1034`; conforme definido para a formatação YES/NO, qualquer valor diferente de zero (0) é um YES e como o idioma é definido como Spanish, FORMATTED_VALUE é SI.|  
|J|Desativado|FORMAT_STRING é definido como `ON/OFF`, VALUE é definido como 0 e LANGUAGE é definido explicitamente como `1034`; conforme definido para a formatação ON/OFF, qualquer valor equivalente a zero (0) é um OFF e, como o idioma está definido para Spanish, FORMATTED_VALUE é Desativado.|  
|K|Ativado|FORMAT_STRING é definido como `ON/OFF`, VALUE é definido como -312 e LANGUAGE é definido explicitamente como `1034`; conforme definido para a formatação ON/OFF, qualquer valor diferente de zero (0) é um ON e como o idioma é definido como Spanish, FORMATTED_VALUE é Ativado.|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Os resultados, transpostos, quando a consulta MDX acima estava sendo executada com o uso de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] em um servidor e cliente com a localidade 1033, da seguinte forma:  
  
|Membro|FORMATTED_VALUE|Explicação|  
|------------|----------------------|-----------------|  
|A|3/12/1959 6:30:00 AM|FORMAT_STRING é definido implicitamente como `General Date` pela expressão CDate() e LANGUAGE é definido como `1033` (English), herdado do valor de localidade do sistema|  
|B|Quinta-feira, 12 de março de 1959|FORMAT_STRING é definido explicitamente como `Long Date` e LANGUAGE é `1033` (English), herdado do valor de localidade do sistema.|  
|C|12/03/1959 6:30:00|FORMAT_STRING é definido explicitamente para `General Date` e LANGUAGE é explicitamente `1034` (Spanish).<br /><br /> Observe que o mês e o dia são alternados quando comparados com o estilo de formatação dos EUA|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING é definido explicitamente para `Long Date` e LANGUAGE é explicitamente `1034` (Spanish).<br /><br /> Observe que o mês e o dia da semana estão em espanhol|  
|E|1959/03/12 6:30:00|FORMAT_STRING é definido explicitamente para `General Date` e LANGUAGE é explicitamente `1041` (japonês).<br /><br /> Observe que a data agora está formatada como Ano/Mês/Dia Hora:Minutos:Segundos|  
|F|1959年3月12日|FORMAT_STRING é definido explicitamente para `Long Date` e LANGUAGE é explicitamente `1041` (japonês).|  
|G|6:30:00 AM|FORMAT_STRING é definido explicitamente como `Long Time` e LANGUAGE é `1033` (English), herdado do valor de localidade do sistema.|  
|H|06:30|FORMAT_STRING é definido explicitamente como `Short Time` e LANGUAGE é `1033` (English), herdado do valor de localidade do sistema.|  
|I|6:30:00|FORMAT_STRING é definido explicitamente para `Long Time` e LANGUAGE é definido explicitamente como `1034` (Spanish).|  
|J|06:30|FORMAT_STRING é definido explicitamente para `Short Time` e LANGUAGE é definido explicitamente como `1034` (Spanish).|  
|K|6:30:00|FORMAT_STRING é definido explicitamente para `Long Time` e LANGUAGE é explicitamente `1041` (Japanese).|  
|L|06:30|FORMAT_STRING é definido explicitamente para `Short Time` e LANGUAGE é explicitamente `1041` (Japanese).|  
  
## <a name="see-also"></a>Consulte também  
 [Conteúdo de FORMAT_STRING & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [Usando propriedades de célula & #40; MDX & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Criando e usando valores de propriedade & #40; MDX & #41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [Conceitos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
