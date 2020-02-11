---
title: Literais de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e90f7683c13d8693529c60f1ba893bd645920bb2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041914"
---
# <a name="interval-literals"></a>Literais de intervalo
O ODBC requer que todos os drivers ofereçam suporte à conversão do tipo de dados SQL_CHAR ou SQL_VARCHAR para todos os tipos de dados de intervalo de C. No entanto, se a fonte de dados subjacente não oferecer suporte a tipos de dados de intervalo, o driver precisará saber o formato correto do valor no campo SQL_CHAR para dar suporte a essas conversões. Da mesma forma, o ODBC requer que qualquer tipo ODBC C seja conversível para SQL_CHAR ou SQL_VARCHAR, portanto, um driver precisa saber qual formato um intervalo armazenado no campo de caractere deve ter. Esta seção descreve a sintaxe de literais de intervalo, que o gravador de driver precisa usar para validar os campos de SQL_CHAR durante a conversão de para ou de tipos de dados de intervalo C.  
  
> [!NOTE]  
>  A sintaxe BNF completa para literais de intervalo é mostrada na [sintaxe literal de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) de seção no Apêndice C: gramática SQL.  
  
 Para passar literais de intervalo como parte de uma instrução SQL, uma sintaxe de cláusula de escape é definida para literais de intervalo. Para obter mais informações, consulte [data, hora e literais de carimbo](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)de hora.  
  
 Um literal de intervalo é do formato:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 em que "INTERVAL" indica que o literal de caractere é um intervalo. O sinal pode ser mais ou menos; Ele está fora da cadeia de caracteres de intervalo e é opcional.  
  
 O qualificador de intervalo pode ser um único campo DateTime ou ser composto por dois campos DateTime, no formato: \<o *campo principal*> \<ao *campo à direita*>.  
  
-   Quando o intervalo é composto por um único campo, o único campo pode ser um campo que não seja um segundo que pode ser acompanhado por uma precisão de entrelinha opcional entre parênteses. O campo DateTime único também pode ser um segundo campo que pode ser acompanhado pela precisão líder opcional, a precisão fracionária opcional de segundos entre parênteses ou ambos. Se a precisão à esquerda e uma precisão fracionária de segundos estiverem presentes por um campo de segundos, elas serão separadas por vírgulas. Se o campo segundos tiver uma precisão fracionária de segundos, ele também deverá ter uma precisão à esquerda.  
  
-   Quando o intervalo é composto de campos à esquerda e à direita, o campo principal é um campo que não é um segundo que pode ser acompanhado pela precisão de campo à esquerda do intervalo entre parênteses. O campo à direita pode ser um campo que não seja um segundo ou um segundo campo que pode ser acompanhado por uma precisão fracionária de segundos de intervalo entre parênteses.  
  
 A cadeia de caracteres do intervalo em *valor* é colocada entre aspas simples. Pode ser um literal de ano/mês ou um literal de dia-hora. O formato da cadeia de caracteres em *valor* é determinado pelas seguintes regras:  
  
-   A cadeia de caracteres contém um valor decimal para cada campo que é implícito pelo \< ** *qualificador* de intervalo>.  
  
-   Se a precisão do intervalo incluir os campos ano e mês, os valores desses campos serão separados por um sinal de subtração.  
  
-   Se a precisão do intervalo incluir os campos dia e hora, os valores desses campos serão separados por um espaço.  
  
-   Se a precisão do intervalo incluir a hora do campo e os campos de ordem inferior (minuto e segundo), os valores desses campos serão separados por dois-pontos.  
  
-   Se a precisão do intervalo incluir um segundo campo e a precisão de segundos expressa ou implícita for diferente de zero, o caractere imediatamente antes do primeiro dígito da parte fracionária do segundo é um ponto.  
  
-   Nenhum campo pode ter mais de dois dígitos, exceto:  
  
    -   O valor do campo principal pode ser tão longo quanto a precisão do intervalo expresso ou implícita.  
  
    -   A parte fracionária do segundo campo pode ser contanto que a precisão de segundos expressa ou implícita.  
  
    -   Os campos à direita seguem as restrições usuais do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 A tabela a seguir lista exemplos de literais de intervalo válidos, conforme incluído na cláusula ODBC Escape para intervalos. A sintaxe da cláusula escape é a seguinte:  
  
> [!NOTE]  
>  *{Intervalo de sinal de intervalo-intervalo de cadeia de caracteres-qualificador}*  
  
|Cláusula de escape literal|Intervalo especificado|  
|---------------------------|------------------------|  
|{INTERVAL ' 326 ' ANO (4)}|Especifica um intervalo de 326 anos. A precisão à esquerda do intervalo é 4.|  
|{INTERVAL ' 326 ' MÊS (3)}|Especifica um intervalo de 326 meses. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL ' 3261 ' DIA (4)}|Especifica um intervalo de 3261 dias. A precisão à esquerda do intervalo é 4.|  
|{INTERVAL ' 163 ' HORA (3)}|Especifica um intervalo de 163 dias. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL ' 163 ' MINUTO (3)}|Especifica um intervalo de 163 minutos. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL ' 223,16 ' SEGUNDO (3, 2)}|Especifica um intervalo de 223,16 segundos. A precisão à esquerda do intervalo é 3 e a precisão de segundos é 2.|  
|{INTERVAL ' 163-11 ' ANO (3) PARA MÊS}|Especifica um intervalo de 163 anos e 11 meses. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL ' 163 12 ' DAY (3) A HOUR}|Especifica um intervalo de 163 dias e 12 horas. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL ' 163 12:39 ' DAY (3) PARA MINUTE}|Especifica um intervalo de 163 dias, 12 horas e 39 minutos. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL "163 12:39:59.163" DAY (3) TO SECOND (3)}|Especifica um intervalo de 163 dias, 12 horas, 39 minutos e 59,163 segundos. A precisão à esquerda do intervalo é 3 e a precisão de segundos é 3.|  
|{INTERVAL ' 163:39 ' HORA (3) PARA MINUTO}|Especifica um intervalo de 163 horas e 39 minutos. A precisão à esquerda do intervalo é 3.|  
|{INTERVAL ' 163:39:59.163 ' HORA (3) A SEGUNDO (4)}|Especifica um intervalo de 163 horas, 39 minutos e 59,163 segundos. A precisão à esquerda do intervalo é 3 e a precisão de segundos é 4.|  
|{INTERVAL ' 163:59.163 ' MINUTO (3) A SEGUNDO (5)}|Especifica um intervalo de 163 minutos e 59,163 segundos. A precisão à esquerda do intervalo é 3 e a precisão de segundos é 5.|  
|{INTERVAL-' 16 23:39:56.23 ' DIA A SEGUNDO}|Especifica um intervalo de menos 16 dias, 23 horas, 39 minutos e 56,23 segundos. A precisão líder implícita é 2, e a precisão de segundos implícita é 6.|  
  
 A tabela a seguir lista exemplos de literais de intervalo inválidos:  
  
|Cláusula de escape literal|Motivo pelo qual o inválido|  
|---------------------------|------------------------|  
|{INTERVAL ' 163 ' HORA (2)}|A precisão à esquerda do intervalo é 2, mas o valor do campo principal é 163.|  
|{INTERVAL ' 223,16 ' SEGUNDO (2, 2)}<br /><br /> {INTERVAL ' 223,16 ' SEGUNDO (3, 1)}|No primeiro exemplo, a precisão à esquerda é muito pequena e, no segundo exemplo, a precisão de segundos é muito pequena.|  
|{INTERVAL ' 223,16 ' SEGUNDO}<br /><br /> {INTERVAL ' 223 ' ANO}|Como a precisão à esquerda não é especificada, o padrão é 2, o que é muito pequeno para manter o literal especificado.|  
|{INTERVAL ' 22,1234567 ' SEGUNDO}|A precisão de segundos não é especificada, portanto, o padrão é 6. O literal tem sete dígitos após o ponto decimal.|  
|{INTERVAL ' 163-13 ' ANO (3) PARA MÊS}<br /><br /> {INTERVAL ' 163 65 ' DAY (3) A HOUR}<br /><br /> {INTERVAL ' 163 62:39 ' DAY (3) PARA MINUTE}<br /><br /> {INTERVAL ' 163 12:125:59.163 ' DAY (3) PARA SECOND (3)}<br /><br /> {INTERVAL ' 163:144 ' HORA (3) PARA MINUTO}<br /><br /> {INTERVAL ' 163:567:234.163 ' HORA (3) A SEGUNDO (4)}<br /><br /> {INTERVAL ' 163:591.163 ' MINUTO (3) A SEGUNDO (5)}|O campo à direita não segue as regras do calendário gregoriano.|
