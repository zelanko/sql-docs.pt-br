---
title: Interval Literals | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1761ac0acb57b3f375a7d19e9371384c000eca5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304937"
---
# <a name="interval-literals"></a>Literais de intervalo
O ODBC exige que todos os drivers suportem a conversão do SQL_CHAR ou SQL_VARCHAR tipo de dados para todos os tipos de dados de intervalo C. No entanto, se a fonte de dados subjacente não suportar os tipos de dados de intervalo, o driver precisa saber o formato correto do valor no campo SQL_CHAR para suportar essas conversões. Da mesma forma, o ODBC exige que qualquer tipo De ODBC C seja conversível para SQL_CHAR ou SQL_VARCHAR, de modo que um motorista precisa saber qual formato um intervalo armazenado no campo de caracteres deve ter. Esta seção descreve a sintaxe de literais de intervalo, que o autor do driver precisa usar para validar os campos SQL_CHAR durante a conversão para ou a partir de tipos de dados de intervalo C.  
  
> [!NOTE]  
>  A sintaxe bnf completa para literais de intervalo é mostrada na seção [Sintaxe Literal do Intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) no Apêndice C: Gramática SQL.  
  
 Para passar literais de intervalo como parte de uma declaração SQL, uma sintaxe de cláusula de escape é definida para literais de intervalo. Para obter mais informações, consulte [Data, Hora e Carimbo de Data](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Um intervalo literal é da forma:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 onde "INTERVAL" indica que o caractere literal é um intervalo. O sinal pode ser mais ou menos; está fora da seqüência de intervalos e é opcional.  
  
 O qualificador de intervalo pode ser um único campo de data-hora \<ou ser \<composto por dois campos de data-hora, na forma: campo *líder*> TO campo de *partida*>.  
  
-   Quando o intervalo é composto por um único campo, o campo único pode ser um campo não-segundo que pode ser acompanhado por uma precisão líder opcional entre parênteses. O campo de data-hora único também pode ser um segundo campo que pode ser acompanhado pela precisão líder opcional, a precisão opcional de fracionamento sumário entre parênteses, ou ambos. Se uma precisão de liderança e uma precisão de segundos fracionados estiverem presentes por um campo de segundos, elas serão separadas por vírgulas. Se o campo de segundos tiver uma precisão de segundos fracionados, ele também deve ter uma precisão de liderança.  
  
-   Quando o intervalo é composto por campos de liderança e de arrasto, o campo principal é um campo não-segundo que pode ser acompanhado pela precisão de campo líder do intervalo entre parênteses. O campo de arrasto pode ser um campo não-segundo ou um segundo campo que pode ser acompanhado por uma precisão de intervalo de segundos fracionados entre parênteses.  
  
 A seqüência de intervalo *sumida* em valor é incluída entre aspas únicas. Pode ser um ano de literal ou um dia literal. O formato da seqüência de *valor* é determinado pelas seguintes regras:  
  
-   A seqüência contém um valor decimal para \<cada campo que está implícito pelo *> de qualificação* *de intervalo.*  
  
-   Se a precisão do intervalo incluir os campos ANO e MÊS, os valores desses campos serão separados por um sinal de menos.  
  
-   Se a precisão do intervalo incluir os campos DIA e HORA, os valores desses campos serão separados por um espaço.  
  
-   Se a precisão do intervalo incluir o campo HORA e os campos de ordem inferior (MINUTO e SEGUNDO), os valores desses campos são separados por um cólon.  
  
-   Se a precisão do intervalo incluir um campo SEGUNDO e a precisão expressa ou implícita de segundos não for zero, o caractere imediatamente antes do primeiro dígito da parte fracionada do segundo é um período.  
  
-   Nenhum campo pode ter mais de dois dígitos de comprimento, exceto:  
  
    -   O valor do campo líder pode ser tão longo quanto a precisão de liderança expressa ou implícita do intervalo.  
  
    -   A parte fracionada do campo SEGUNDO pode ser tão longa quanto a precisão expressa ou implícita de segundos.  
  
    -   Os campos de perseguição seguem as restrições habituais do calendário gregoriano. (Veja [as restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 A tabela a seguir lista exemplos de literais de intervalo válidos incluídos na cláusula de escape oDBC para intervalos. A sintaxe da cláusula de fuga é a seguinte:  
  
> [!NOTE]  
>  *{INTERVAL sign interval-string interval-qualifier}*  
  
|Cláusula de fuga literal|Intervalo especificado|  
|---------------------------|------------------------|  
|{INTERVALO '326' ANO(4)}|Especifica um intervalo de 326 anos. A precisão de intervalo é 4.|  
|{INTERVALO '326' MÊS(3)}|Especifica um intervalo de 326 meses. A precisão de intervalo é 3.|  
|{INTERVALO '3261' DIA(4)}|Especifica um intervalo de 3261 dias. A precisão de intervalo é 4.|  
|{INTERVALO '163' HORA(3)}|Especifica um intervalo de 163 dias. A precisão de intervalo é 3.|  
|{INTERVALO '163' MINUTO(3)}|Especifica um intervalo de 163 minutos. A precisão de intervalo é 3.|  
|{INTERVALO '223.16' SEGUNDO(3,2)}|Especifica um intervalo de 223,16 segundos. A precisão de intervalo é 3, e a precisão dos segundos é de 2.|  
|{INTERVALO '163-11' ANO(3) A MÊS}|Especifica um intervalo de 163 anos e 11 meses. A precisão de intervalo é 3.|  
|{INTERVALO '163 12' DIA(3) A HORA}|Especifica um intervalo de 163 dias e 12 horas. A precisão de intervalo é 3.|  
|{INTERVALO '163 12:39' DIA(3) A MINUTO}|Especifica um intervalo de 163 dias, 12 horas e 39 minutos. A precisão de intervalo é 3.|  
|{INTERVALO '163 12:39:59.163' DIA(3) PARA SEGUNDO(3)}|Especifica um intervalo de 163 dias, 12 horas, 39 minutos e 59,163 segundos. A precisão de intervalo é 3, e a precisão dos segundos é 3.|  
|{INTERVALO '163:39' HORA(3) A MINUTO}|Especifica um intervalo de 163 horas e 39 minutos. A precisão de intervalo é 3.|  
|{INTERVALO '163:39:59.163' HORA(3) PARA SEGUNDO(4)}|Especifica um intervalo de 163 horas, 39 minutos e 59.163 segundos. A precisão de intervalo é 3, e a precisão dos segundos é 4.|  
|{INTERVALO '163:59.163' MINUTO(3) PARA SEGUNDO(5)}|Especifica um intervalo de 163 minutos e 59.163 segundos. A precisão de intervalo é 3, e a precisão dos segundos é de 5.|  
|{INTERVALO -'16 23:39:56.23' DIA A SEGUNDO}|Especifica um intervalo de menos 16 dias, 23 horas, 39 minutos e 56,23 segundos. A precisão de liderança implícita é 2, e a precisão implícita de segundos é 6.|  
  
 A tabela a seguir lista exemplos de literais de intervalo inválido:  
  
|Cláusula de fuga literal|Razão pela qual inválido|  
|---------------------------|------------------------|  
|{INTERVALO '163' HORA(2)}|A precisão de intervalo é 2, mas o valor do campo principal é de 163.|  
|{INTERVALO '223.16' SEGUNDO(2,2)}<br /><br /> {INTERVALO '223.16' SEGUNDO(3,1)}|No primeiro exemplo, a precisão principal é muito pequena, e no segundo exemplo, a precisão dos segundos é muito pequena.|  
|{INTERVALO '223.16' SEGUNDO}<br /><br /> {INTERVALO '223' ANO}|Como a precisão principal não é especificada, ela é padrão para 2, que é muito pequena para segurar o literal especificado.|  
|{INTERVALO '22.1234567' SEGUNDO}|A precisão dos segundos não é especificada, por isso é padrão para 6. O literal tem sete dígitos após o ponto decimal.|  
|{INTERVALO '163-13' ANO(3) A MÊS}<br /><br /> {INTERVALO '163 65' DIA(3) A HORA}<br /><br /> {INTERVALO '163 62:39' DIA(3) A MINUTO}<br /><br /> {INTERVALO '163 12:125:59.163' DIA(3) PARA SEGUNDO(3)}<br /><br /> {INTERVALO '163:144' HORA(3) A MINUTO}<br /><br /> {INTERVALO '163:567:234.163' HORA(3) PARA SEGUNDO(4)}<br /><br /> {INTERVALO '163:591.163' MINUTO(3) PARA SEGUNDO(5)}|O campo de perseguição não segue as regras do calendário gregoriano.|
