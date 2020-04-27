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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284756"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restrições do calendário gregoriano
Os tipos de dados Date e DateTime, e os campos à direita dos tipos de dados Interval, devem estar em conformidade com as restrições do calendário gregoriano. Essas restrições são as seguintes:  
  
-   O valor do campo mês deve estar entre 1 e 12, inclusive.  
  
-   O valor do campo dia deve estar no intervalo entre 1 e o número de dias do mês. O número de dias no mês é determinado dos valores dos campos year e months e pode ser 28, 29, 30 ou 31. (O número de dias no mês também pode depender se é um ano bissexto.)  
  
-   O valor do campo de hora deve estar entre 0 e 23, inclusive.  
  
-   O valor do campo de minuto deve estar entre 0 e 59, inclusive.  
  
-   Para o campo segundos à direita dos tipos de dados de intervalo, o valor do campo segundos deve estar entre 0 e 59,9 (*n*), inclusive, em que *n* é o número de dígitos na precisão de segundos fracionários.  
  
-   Para o campo segundos à direita dos tipos de dados DateTime, o valor do campo segundos deve estar entre 0 e 61,9 (*n*), inclusive, em que *n* especifica o número de dígitos "9" e o valor de *n* é a precisão de segundos fracionários. (O intervalo de segundos permite que até dois segundos bissextos mantenham a sincronização do tempo de Sidereal.)
