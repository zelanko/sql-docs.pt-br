---
title: "Sequências de escape | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c648549b41ff607ad34175475c6a2b75603625f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="escape-sequences"></a>Sequências de escape
ODBC define sequências de escape que contém a gramática padrão para data, hora, timestamp e literais de intervalo de data e hora, chamadas de função escalar, **como** predicado caracteres de escape, junções externas e chamadas de procedimento. Aplicativos interoperáveis devem usar essas sequências sempre que possível.  
  
 Para determinar se um driver suporta as sequências de escape para data, hora, carimbo de hora ou literais de intervalo de data e hora, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados oferece suporte a uma data, hora, timestamp ou tipo de dados de intervalo de data e hora, ele também deve oferecer suporte a sequência de escape correspondente. Para determinar se as sequências de escape têm suporte, um aplicativo chama **SQLGetInfo**.  
  
 Para obter mais informações, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), mais adiante nesta seção.

