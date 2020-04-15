---
title: Restrições do Calendário Gregoriano | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284756"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restrições do calendário gregoriano
Os tipos de dados de data e data e data, e os campos de dados de intervalo, devem estar em conformidade com as restrições do calendário gregoriano. Essas restrições são as seguintes:  
  
-   O valor do campo mensal deve ser entre 1 e 12, inclusive.  
  
-   O valor do campo diurno deve estar na faixa de 1 até o número de dias no mês. O número de dias no mês é determinado a partir dos valores dos campos do ano e meses e pode ser de 28, 29, 30 ou 31. (O número de dias no mês também pode depender se é um ano bissexto.)  
  
-   O valor do campo de horas deve ser entre 0 e 23, inclusive.  
  
-   O valor do campo de minutos deve ser entre 0 e 59, inclusive.  
  
-   Para o campo de segundos de seguimento dos tipos de dados de intervalo, o valor do campo de segundos deve ser entre 0 e 59,9(n), inclusive, onde *n* é o número de dígitos na precisão de segundos fracionados.*n*  
  
-   Para o campo de segundos de seguimento dos tipos de dados de data-hora, o valor do campo segundos deve ser entre 0 e 61,9(n), inclusive, onde *n* especifica o número de "9" dígitos e o valor de *n* é a precisão de segundos fracionados.*n* (O intervalo de segundos permite até dois segundos de salto para manter a sincronização do tempo sidereal.)
