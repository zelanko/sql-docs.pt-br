---
title: Sequências de escape | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1423d7bcc0f0b943b490fdcf8f931efb6b533c6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259271"
---
# <a name="escape-sequences"></a>Sequências de escape
ODBC define sequências de escape que contém a gramática padrão para chamadas de função escalar de data, hora, carimbo de hora e literais de intervalo de data e hora **como** predicado caracteres de escape, junções externas e chamadas de procedimento. Aplicativos interoperáveis devem usar essas sequências sempre que possível.  
  
 Para determinar se um driver suporta as sequências de escape para data, hora, carimbo de hora ou literais de intervalo de data e hora, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados oferece suporte a uma data, hora, timestamp ou tipo de dados de intervalo de data e hora, ele também deverá dar suporte a sequência de escape correspondente. Para determinar se as outras sequências de escape são compatíveis, um aplicativo chama **SQLGetInfo**.  
  
 Para obter mais informações, consulte [sequências de Escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), mais adiante nesta seção.
