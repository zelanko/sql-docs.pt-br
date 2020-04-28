---
title: Tipos de dados de intervalo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ee4a6e845e0bc0830f514b2e768075dd75bcf6e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304962"
---
# <a name="interval-data-types"></a>Tipo de dados de intervalo
Um intervalo é definido como a diferença entre duas datas e horas. Os intervalos são expressos de uma das duas maneiras diferentes. Um é um intervalo de *ano-mês* que expressa intervalos em termos de anos e um número integral de meses. O outro é um intervalo de *dia-hora* que expressa intervalos em termos de dias, minutos e segundos. Esses dois tipos de intervalos são distintos e não podem ser misturados, pois os meses podem ter diversos números de dias.  
  
 Um intervalo consiste em um conjunto de campos. Há uma ordenação implícita entre os campos. Por exemplo, em um intervalo de ano a mês, o ano vem primeiro, seguido pelo mês. Da mesma forma, em um intervalo de dia a minuto, os campos estão no dia do pedido, na hora e no minuto. O primeiro campo em um tipo de intervalo é chamado de campo *principal* , ou o campo de *ordem superior* . O último campo é chamado de campo *à direita* .  
  
 Em todos os intervalos, o campo principal não é restrito por regras do calendário gregoriano. Por exemplo, em um intervalo de hora a minuto, o campo de hora não é restrito para estar entre 0 e 23 (inclusivo), como normalmente é. Os campos à direita subsequentes para o campo à esquerda seguem as restrições usuais do calendário gregoriano. Para obter mais informações, consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais adiante neste apêndice.  
  
 Há 13 tipos de dados SQL de intervalo e tipos de dados de 13 intervalos C. Cada um dos tipos de dados do intervalo C usa a mesma estrutura, SQL_INTERVAL_STRUCT, para conter os dados do intervalo. (Para obter mais informações, consulte a próxima seção, [estrutura de intervalo de C](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obter mais informações sobre os tipos de dados SQL, consulte [tipos de dados SQL](../../../odbc/reference/appendixes/sql-data-types.md); para obter mais informações sobre os tipos de dados C, consulte [tipos de dados c](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Classe|Descrição|  
|---------------------|-----------|-----------------|  
|MONTH|Ano-mês|Número de meses entre duas datas.|  
|YEAR|Ano-mês|Número de anos entre duas datas.|  
|YEAR_TO_MONTH|Ano-mês|Número de anos e meses entre duas datas.|  
|DAY|Dia e hora|Número de dias entre duas datas.|  
|HOUR|Dia e hora|Número de horas entre duas datas/horas.|  
|MINUTE|Dia e hora|Número de minutos entre duas datas/horas.|  
|SECOND|Dia e hora|Número de segundos entre duas datas/horas.|  
|DAY_TO_HOUR|Dia e hora|Número de dias/horas entre duas data/hora.|  
|DAY_TO_MINUTE|Dia e hora|Número de dias/horas/minutos entre duas data/hora.|  
|DAY_TO_SECOND|Dia e hora|Número de dias/horas/minutos/segundos entre duas datas/horas.|  
|HOUR_TO_MINUTE|Dia e hora|Número de horas/minutos entre duas datas/horas.|  
|HOUR_TO_SECOND|Dia e hora|Número de horas/minutos/segundos entre duas datas/horas.|  
|MINUTE_TO_SECOND|Dia e hora|Número de minutos/segundos entre duas datas/horas.|  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Estrutura de intervalo do C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisão do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literais de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Substituindo precisão inicial e de segundos padrão para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
