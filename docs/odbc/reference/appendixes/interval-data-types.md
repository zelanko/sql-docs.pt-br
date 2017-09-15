---
title: Tipos de dados de intervalo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- second intervals [ODBC]
- data types [ODBC], interval data types
- interval data type [ODBC]
- day-time intervals [ODBC]
- intervals [ODBC], about intervals
- minute intervals [ODBC]
- day intervals [ODBC]
- year intervals [ODBC]
- month intervals [ODBC]
- interval data type [ODBC], about interval data types
- SQL data types [ODBC], interval
- year-month intervals [ODBC]
- C data types [ODBC], interval
- interval fields [ODBC]
ms.assetid: fba93f65-c1db-44f4-91ba-532f87241cf7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1e19ac3f7c14326524ab7cbaa60f499c5d81e91
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="interval-data-types"></a>Tipos de dados de intervalo
Um intervalo é definido como a diferença entre duas datas e horas. Intervalos são expressos em uma das duas maneiras diferentes. Um é um *ano-mês* intervalo que expressa intervalos em termos de anos e um número integral de meses. A outra é um *dia hora* intervalo que expressa intervalos em termos de dias, minutos e segundos. Esses dois tipos de intervalos são diferentes e não podem ser misturados, como meses podem ter diferentes números de dias.  
  
 Um intervalo consiste em um conjunto de campos. Há uma ordenação implícita entre os campos. Por exemplo, em um intervalo de ano-mês, ano vier primeiro, seguido por mês. Da mesma forma, em um intervalo de dias para minutos, os campos estão na ordem dia, hora e minuto. O primeiro campo em um tipo de intervalo é chamado de *principal* campo, ou o *superiores* campo. O último campo é chamado de *à direita* campo.  
  
 Em todos os intervalos, o campo à esquerda não é restrito pelas regras do calendário gregoriano. Por exemplo, em um intervalo de hora-minuto, o campo de hora não está restrito a ser entre 0 e 23 (inclusive), que normalmente é. Os campos à direita após o campo principal execute as restrições normais do calendário gregoriano. Para obter mais informações, consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais adiante neste apêndice.  
  
 Há 13 tipos de dados SQL de intervalo e 13 tipos de dados C de intervalo. Cada um dos tipos de dados de intervalo C usa a mesma estrutura, SQL_INTERVAL_STRUCT, para conter os dados de intervalo. (Para obter mais informações, consulte a próxima seção, [C intervalo estrutura](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obter mais informações sobre os tipos de dados SQL, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md); para obter mais informações sobre os tipos de dados C, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Classe|Description|  
|---------------------|-----------|-----------------|  
|MONTH|Mês do ano|Número de meses entre duas datas.|  
|YEAR|Mês do ano|Número de anos entre duas datas.|  
|YEAR_TO_MONTH|Mês do ano|Número de anos e meses entre duas datas.|  
|DAY|Hora do dia|Número de dias entre duas datas.|  
|HOUR|Hora do dia|Número de horas entre dois data/horas.|  
|MINUTE|Hora do dia|Número de minutos entre dois data/horas.|  
|SECOND|Hora do dia|Número de segundos entre dois data/horas.|  
|DAY_TO_HOUR|Hora do dia|Número de dias/horas entre dois data/horas.|  
|DAY_TO_MINUTE|Hora do dia|Número de dias/horas/minutos entre dois data/horas.|  
|DAY_TO_SECOND|Hora do dia|Número de dias/horas/minutos/segundos entre dois data/horas.|  
|HOUR_TO_MINUTE|Hora do dia|Número de horas/minutos entre dois data/horas.|  
|HOUR_TO_SECOND|Hora do dia|Número de horas/minutos/segundos entre dois data/horas.|  
|MINUTE_TO_SECOND|Hora do dia|Número de minutos/segundos entre dois data/horas.|  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Estrutura de intervalo do C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisão do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literais de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Substituindo precisão inicial e de segundos padrão para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
