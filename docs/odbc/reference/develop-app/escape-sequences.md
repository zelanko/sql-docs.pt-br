---
title: Sequências de escape | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9bb389cba92f45373e7fc693c9c4477d50a702a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="escape-sequences"></a>Sequências de escape
ODBC define sequências de escape que contém a gramática padrão para data, hora, timestamp e literais de intervalo de data e hora, chamadas de função escalar, **como** predicado caracteres de escape, junções externas e chamadas de procedimento. Aplicativos interoperáveis devem usar essas sequências sempre que possível.  
  
 Para determinar se um driver suporta as sequências de escape para data, hora, carimbo de hora ou literais de intervalo de data e hora, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados oferece suporte a uma data, hora, timestamp ou tipo de dados de intervalo de data e hora, ele também deve oferecer suporte a sequência de escape correspondente. Para determinar se as sequências de escape têm suporte, um aplicativo chama **SQLGetInfo**.  
  
 Para obter mais informações, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), mais adiante nesta seção.
