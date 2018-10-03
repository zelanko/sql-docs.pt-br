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
manager: craigg
ms.openlocfilehash: 30fbdd17e7ec5eb970948e1c7133020081222614
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847924"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Restrições do calendário gregoriano
Tipos de dados de data e a data e hora e os campos à direita dos tipos de dados de intervalo, devem estar em conformidade com as restrições do calendário gregoriano. Essas restrições são da seguinte maneira:  
  
-   O valor do campo de mês deve estar entre 1 e 12, inclusive.  
  
-   O valor do campo dia deve ser no intervalo entre 1 e o número de dias no mês. O número de dias do mês é determinado a partir de valores dos campos de ano e meses e pode ser 28, 29, 30 ou 31. (O número de dias no mês também pode depender se ele é um ano bissexto.)  
  
-   O valor do campo de hora deve estar entre 0 e 23, inclusive.  
  
-   O valor do campo minuto deve estar entre 0 e 59, inclusive.  
  
-   Para o campo de segundos à direita dos tipos de dados de intervalo, o valor do campo de segundos deve estar entre 0 e 59.9 (*n*), inclusive, onde *n* é o número de dígitos na precisão de frações de segundo.  
  
-   Para o campo de segundos à direita dos tipos de dados de data e hora, o valor do campo de segundos deve estar entre 0 e 61.9 (*n*), inclusive, onde *n* Especifica o número de dígitos "9" e o valor de *n*  é a precisão de frações de segundo. (O intervalo de segundos permite até dois segundos intercalares para manter a sincronização de tempo de sidereal).
