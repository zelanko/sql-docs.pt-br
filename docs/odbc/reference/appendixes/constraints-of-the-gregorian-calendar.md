---
title: "Restrições do calendário gregoriano | Microsoft Docs"
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
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1b149b1e9df8338b5502d57e6e7eb355b66bcc3f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="constraints-of-the-gregorian-calendar"></a>Restrições do calendário gregoriano
Tipos de dados de data e a data e hora e os campos à direita dos tipos de dados de intervalo, devem estar de acordo com as restrições do calendário gregoriano. Essas restrições são os seguintes:  
  
-   O valor do campo mês deve estar entre 1 e 12, inclusive.  
  
-   O valor do campo dia deve ser no intervalo entre 1 e o número de dias do mês. O número de dias do mês é determinado a partir de valores dos campos de ano e meses e pode ser 28, 29, 30 ou 31. (O número de dias no mês pode também dependem se é um ano bissexto.)  
  
-   O valor do campo de hora deve estar entre 0 e 23, inclusive.  
  
-   O valor do campo minuto deve estar entre 0 e 59, inclusive.  
  
-   Para o campo de segundos à direita dos tipos de dados de intervalo, o valor do campo de segundos deve estar entre 0 e 59.9 (*n*), inclusive, onde  *n*  é o número de dígitos a precisão de frações de segundo.  
  
-   Para o campo de segundos à direita dos tipos de dados de data e hora, o valor do campo de segundos deve estar entre 0 e 61.9 (*n*), inclusive, onde  *n*  Especifica o número de "9" dígitos e o valor de  *n*  é a precisão de frações de segundo. (O intervalo de segundos permite até dois segundos intercalares para manter a sincronização de tempo de sidereal).

