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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304962"
---
# <a name="interval-data-types"></a>Tipo de dados de intervalo
Um intervalo é definido como a diferença entre duas datas e horários. Os intervalos são expressos de uma das duas maneiras diferentes. Um deles é um intervalo *de um ano* que expressa intervalos em termos de anos e um número integral de meses. O outro é um intervalo *diurno* que expressa intervalos em termos de dias, minutos e segundos. Esses dois tipos de intervalos são distintos e não podem ser misturados, pois meses podem ter números variados de dias.  
  
 Um intervalo consiste em um conjunto de campos. Há uma ordem implícita entre os campos. Por exemplo, em um intervalo de um ano para o mês, o ano vem em primeiro lugar, seguido pelo mês. Da mesma forma, em um intervalo de dia a minuto, os campos estão na ordem dia, hora e minuto. O primeiro campo em um tipo de intervalo é chamado de campo *principal,* ou campo *de alta ordem.* O último campo é chamado de campo *de perseguição.*  
  
 Em todos os intervalos, o campo principal não é constrangido pelas regras do calendário gregoriano. Por exemplo, em um intervalo de hora para minuto, o campo de horas não é limitado a ser entre 0 e 23 (inclusive), como normalmente é. Os campos de perseguição posteriores ao campo principal seguem as restrições habituais do calendário gregoriano. Para obter mais informações, consulte [Restrições do Calendário Gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), mais tarde neste apêndice.  
  
 Existem 13 tipos de dados SQL de intervalo e 13 tipos de dados de intervalo C. Cada um dos tipos de dados do intervalo C usa a mesma estrutura, SQL_INTERVAL_STRUCT, para conter os dados de intervalo. (Para obter mais informações, consulte a próxima seção, [C Interval Structure](../../../odbc/reference/appendixes/c-interval-structure.md).) Para obter mais informações sobre os tipos de dados SQL, consulte [tipos de dados SQL;](../../../odbc/reference/appendixes/sql-data-types.md) para obter mais informações sobre os tipos de dados C, consulte [C Data Types](../../../odbc/reference/appendixes/c-data-types.md).  
  
|Identificador de tipo|Classe|Descrição|  
|---------------------|-----------|-----------------|  
|MONTH|Mês do Ano|Número de meses entre duas datas.|  
|YEAR|Mês do Ano|Número de anos entre duas datas.|  
|YEAR_TO_MONTH|Mês do Ano|Número de anos e meses entre duas datas.|  
|DAY|Dia- a- dia|Número de dias entre duas datas.|  
|HOUR|Dia- a- dia|Número de horas entre duas datas/horários.|  
|MINUTE|Dia- a- dia|Número de minutos entre duas datas/horários.|  
|SECOND|Dia- a- dia|Número de segundos entre duas datas/horários.|  
|DAY_TO_HOUR|Dia- a- dia|Número de dias/horas entre duas datas/horários.|  
|DAY_TO_MINUTE|Dia- a- dia|Número de dias/horas/minutos entre duas datas/horários.|  
|DAY_TO_SECOND|Dia- a- dia|Número de dias/horas/minutos/segundos entre duas datas/horários.|  
|HOUR_TO_MINUTE|Dia- a- dia|Número de horas/minutos entre duas datas/horários.|  
|HOUR_TO_SECOND|Dia- a- dia|Número de horas/minutos/segundos entre duas datas/horários.|  
|MINUTE_TO_SECOND|Dia- a- dia|Número de minutos/segundos entre duas datas/horários.|  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Estrutura de intervalo do C](../../../odbc/reference/appendixes/c-interval-structure.md)  
  
-   [Precisão do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-precision.md)  
  
-   [Comprimento do tipo de dados de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md)  
  
-   [Literais de intervalo](../../../odbc/reference/appendixes/interval-literals.md)  
  
-   [Substituindo precisão inicial e de segundos padrão para tipos de dados de intervalo](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md)
