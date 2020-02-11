---
title: Restrições do calendário gregoriano | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f67d313f5a1261dba1f88e9ef3a70d30c1cd503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019180"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restrições do calendário gregoriano
Os tipos de dados Date e DateTime, e os campos à direita dos tipos de dados Interval, devem estar em conformidade com as restrições do calendário gregoriano. Essas restrições são as seguintes:  
  
-   O valor do campo mês deve estar entre 1 e 12, inclusive.  
  
-   O valor do campo dia deve estar no intervalo entre 1 e o número de dias do mês. O número de dias no mês é determinado dos valores dos campos year e months e pode ser 28, 29, 30 ou 31. (O número de dias no mês também pode depender se é um ano bissexto.)  
  
-   O valor do campo de hora deve estar entre 0 e 23, inclusive.  
  
-   O valor do campo de minuto deve estar entre 0 e 59, inclusive.  
  
-   Para o campo segundos à direita dos tipos de dados de intervalo, o valor do campo segundos deve estar entre 0 e 59,9 (*n*), inclusive, em que *n* é o número de dígitos na precisão de segundos fracionários.  
  
-   Para o campo segundos à direita dos tipos de dados DateTime, o valor do campo segundos deve estar entre 0 e 61,9 (*n*), inclusive, em que *n* especifica o número de dígitos "9" e o valor de *n* é a precisão de segundos fracionários. (O intervalo de segundos permite que até dois segundos bissextos mantenham a sincronização do tempo de Sidereal.)
