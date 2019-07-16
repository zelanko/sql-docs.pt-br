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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041914"
---
# <a name="interval-literals"></a>Literais de intervalo
O ODBC exige que todos os drivers de suporte à conversão do tipo de dados SQL_CHAR ou SQL_VARCHAR todos os tipos de dados de intervalo de C. Se a fonte de dados subjacente não oferece suporte a tipos de dados de intervalo, no entanto, o driver precisa saber o formato correto do valor no campo SQL_CHAR para dar suporte a essas conversões. Da mesma forma, o ODBC exige que qualquer tipo ser conversível para SQL_CHAR ou SQL_VARCHAR, portanto, um driver precisa saber qual formato de um intervalo armazenado no campo de caractere do ODBC C deve ter. Esta seção descreve a sintaxe de literais de intervalo, o que o gravador de driver precisa ser usado para validar os campos SQL_CHAR durante a conversão para ou de tipos de dados de intervalo de C.  
  
> [!NOTE]  
>  A sintaxe BNF completa para literais de intervalo é mostrada na seção [sintaxe de Literal de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) no Apêndice c: Gramática SQL.  
  
 Para passar os literais de intervalo como parte de uma instrução SQL, uma sintaxe da cláusula de escape é definida para literais de intervalo. Para obter mais informações, consulte [data, hora e literais de carimbo de hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Um literal de intervalo está no formato:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 onde "Intervalo" indica que o literal de caractere é um intervalo. O sinal pode ser mais ou menos; ele está fora de sequência de caracteres do intervalo e é opcional.  
  
 O qualificador de intervalo pode ser um campo datetime único ou ser composto de dois campos de data e hora no formato: \< *à esquerda do campo*> TO \< *à direita do campo*>.  
  
-   Quando o intervalo é composto de um único campo, o único campo pode ser um campo de segundo não pode ser acompanhado por uma precisão opcional à esquerda entre parênteses. O campo de data e hora único também pode ser um segundo campo que pode ser acompanhado por precisão opcional à esquerda, a precisão de segundos fracionários opcionais entre parênteses ou ambos. Se uma precisão à esquerda e uma precisão de segundos fracionários estiverem presentes para um campo de segundos, eles são separados por vírgulas. Se o campo de segundos tem uma precisão fracionária em segundos, ela também deve ter uma precisão à esquerda.  
  
-   Quando o intervalo é composto de campos à esquerda e à direita, o campo à esquerda é um campo de segundo não pode ser acompanhado pelo intervalo de precisão de campo inicial entre parênteses. O campo à direita pode ser um campo de não-segundo ou um segundo campo que pode ser acompanhado por uma precisão de frações de segundos de intervalo entre parênteses.  
  
 A cadeia de caracteres no intervalo *valor* é colocado entre aspas simples. Ele pode ser um literal de ano-mês ou um literal de tempo-dia. O formato da cadeia de caracteres *valor* é determinado pelas seguintes regras:  
  
-   A cadeia de caracteres contém um valor decimal para cada campo implícita a \< *intervalo* *qualificador*>.  
  
-   Se a precisão de intervalo inclui os campos de ano e mês, os valores desses campos são separados por um sinal de subtração.  
  
-   Se a precisão de intervalo inclui os campos de dia e hora, os valores desses campos são separados por um espaço.  
  
-   Se a precisão de intervalo inclui o campo de hora e campos de ordem inferiores (minuto e segundo), os valores desses campos são separados por dois-pontos.  
  
-   Se a precisão de intervalo inclui um segundo campo e a precisão de segundos contratual ou legal é diferente de zero, o caractere imediatamente antes do primeiro dígito da parte fracionária do segundo é um período.  
  
-   Nenhum campo pode ser mais de dois dígitos, exceto:  
  
    -   O valor do campo principal pode ser, desde que o intervalo contratual ou legal precisão inicial.  
  
    -   A parte fracionária do segundo campo pode ser, desde que a precisão de segundos contratual ou legal.  
  
    -   Os campos à direita seguem as restrições comuns do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 A tabela a seguir lista exemplos de literais de intervalo válido como incluídas na cláusula de escape ODBC para intervalos. A sintaxe da cláusula de escape é da seguinte maneira:  
  
> [!NOTE]  
>  *{INTERVALO entrada cadeia de caracteres do intervalo intervalo qualificador}*  
  
|Cláusula de escape literal|Intervalo especificado|  
|---------------------------|------------------------|  
|{YEAR(4) DE INTERVALO '326'}|Especifica um intervalo de anos 326. O intervalo de precisão inicial é 4.|  
|{MONTH(3) DE INTERVALO '326'}|Especifica um intervalo de meses 326. O intervalo de precisão inicial é 3.|  
|{DAY(4) DE INTERVALO '3261'}|Especifica um intervalo de dias 3261. O intervalo de precisão inicial é 4.|  
|{HOUR(3) DE INTERVALO '163'}|Especifica um intervalo de dias 163. O intervalo de precisão inicial é 3.|  
|{MINUTE(3) DE INTERVALO '163'}|Especifica um intervalo de minutos 163. O intervalo de precisão inicial é 3.|  
|{SECOND(3,2) DE INTERVALO '223.16'}|Especifica um intervalo de segundos 223.16. A precisão de intervalo à esquerda é 3, e a precisão de segundos é 2.|  
|{INTERVALO ' 163-11' YEAR(3) AO MÊS}|Especifica um intervalo de 163 anos e 11 meses. O intervalo de precisão inicial é 3.|  
|{INTERVALO 163 ' 12' DAY(3) HORA}|Especifica um intervalo de 163 dias e 12 horas. O intervalo de precisão inicial é 3.|  
|{INTERVALO ' 163 12:39 ' DAY(3) MINUTO}|Especifica um intervalo de 163 dias, 12 horas e 39 minutos. O intervalo de precisão inicial é 3.|  
|{DAY(3) DO INTERVALO '163 12:39:59.163' PARA SECOND(3)}|Especifica um intervalo de 163 dias, 12 horas, 39 minutos e 59.163 segundos. A precisão de intervalo à esquerda é 3, e a precisão de segundos é 3.|  
|{INTERVALO '163:39' HOUR(3) MINUTO}|Especifica um intervalo de 163 horas e 39 minutos. O intervalo de precisão inicial é 3.|  
|{INTERVALO '163:39:59.163' HOUR(3) PARA SECOND(4)}|Especifica um intervalo de 163 horas, 39 minutos e 59.163 segundos. A precisão de intervalo à esquerda é 3, e a precisão de segundos é 4.|  
|{INTERVALO '163:59.163' MINUTE(3) PARA SECOND(5)}|Especifica um intervalo de 163 minutos e 59.163 segundos. A precisão de intervalo à esquerda é 3, e a precisão de segundos é 5.|  
|{INTERVALO - DIA '16 23:39:56.23' PARA O SEGUNDO}|Especifica um intervalo de menos de 16 dias, 23 horas, 39 minutos e 56.23 segundos. A precisão à esquerda implícita é 2, e a precisão de segundos implícita é 6.|  
  
 A tabela a seguir lista exemplos de literais de intervalo inválido:  
  
|Cláusula de escape literal|Motivo por que inválido|  
|---------------------------|------------------------|  
|{HOUR(2) DE INTERVALO '163'}|A precisão de intervalo à esquerda é 2, mas o valor do campo à esquerda é 163.|  
|{SECOND(2,2) DE INTERVALO '223.16'}<br /><br /> {SECOND(3,1) DE INTERVALO '223.16'}|No primeiro exemplo, a precisão à esquerda é muito pequena e, no segundo exemplo, a precisão de segundos é muito pequena.|  
|{INTERVALO '223.16' SEGUNDO}<br /><br /> {INTERVALO '223' ANO}|Porque a precisão à esquerda não for especificada, o padrão é 2, que é muito pequeno para conter o literal especificado.|  
|{INTERVALO '22.1234567' SEGUNDO}|A precisão de segundos é especificada, portanto, o padrão é 6. O literal tem sete dígitos após o ponto decimal.|  
|{INTERVALO ' 163-13' YEAR(3) AO MÊS}<br /><br /> {INTERVALO ' 163 65' DAY(3) HORA}<br /><br /> {DAY(3) DO INTERVALO '163 62:39' MINUTO}<br /><br /> {DAY(3) DO INTERVALO '163 12:125:59.163' PARA SECOND(3)}<br /><br /> {INTERVALO '163:144' HOUR(3) MINUTO}<br /><br /> {INTERVALO '163:567:234.163' HOUR(3) PARA SECOND(4)}<br /><br /> {INTERVALO '163:591.163' MINUTE(3) PARA SECOND(5)}|O campo à direita não segue as regras do calendário gregoriano.|
