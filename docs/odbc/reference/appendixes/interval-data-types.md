---
title: Tipos de dados Interval | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 930a848ea01d128cb248c7929408ce7510937ad9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622214"
---
# <a name="interval-data-types"></a>Tipo de dados de intervalo
Um intervalo é definido como a diferença entre duas datas e horas. Intervalos são expressas em uma das duas maneiras diferentes. Um é um *ano-mês* intervalo que expressa a intervalos em termos de anos e um número integral de meses. O outro é um *tempo-dia* intervalo que expressa a intervalos em termos de dias, minutos e segundos. Esses dois tipos de intervalos são distintos e não podem ser misturados, como meses podem ter diferentes números de dias.  
  
 Um intervalo consiste em um conjunto de campos. Há uma ordenação implícita entre os campos. Por exemplo, em um intervalo de ano para mês, ano vem primeiro, seguido por mês. Da mesma forma, um intervalo de dias para minutos, os campos estão em ordem dia, hora e minuto. O primeiro campo em um tipo de intervalo é chamado de *à esquerda* campo, ou o *ordem alta* campo. O último campo é chamado de *à direita* campo.  
  
 Em todos os intervalos, o campo à esquerda não é restrito pelas regras do calendário gregoriano. Por exemplo, em um intervalo de hora para minuto, o campo de hora não é restrito para ser entre 0 e 23 (inclusive), pois ele é normalmente. Os campos à direita após o campo principal seguem as restrições comuns do calendário gregoriano. Para obter mais informações, consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais adiante neste apêndice.  
  
 Há 13 tipos de dados SQL de intervalo e 13 tipos de dados C de intervalo. Cada um dos tipos de dados de intervalo C usa a mesma estrutura, SQL_INTERVAL_STRUCT, para conter os dados de intervalo. (Para obter mais informações, consulte a próxima seção, [estrutura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obter mais informações sobre os tipos de dados SQL, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md); para obter mais informações sobre os tipos de dados C, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md).  
  
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
