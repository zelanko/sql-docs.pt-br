---
description: Sequências de escape
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15c06fc08d78422502b8aea87c40ee2821a9620f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429298"
---
# <a name="escape-sequences"></a>Sequências de escape
O ODBC define as sequências de escape contendo a gramática padrão para os literais de data, hora, carimbo de data e hora e intervalo de DateTime, chamadas de função escalares, **como** caracteres de escape de predicado, junções externas e chamadas de procedimento. Aplicativos interoperáveis devem usar essas sequências sempre que possível.  
  
 Para determinar se um driver dá suporte a sequências de escape para os literais de data, hora, timestamp ou intervalo de DateTime, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados der suporte a um tipo de dados de data, hora, timestamp ou intervalo de DateTime, ele também deverá oferecer suporte à sequência de escape correspondente. Para determinar se há suporte para as outras sequências de escape, um aplicativo chama **SQLGetInfo**.  
  
 Para obter mais informações, consulte [sequências de escape no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), mais adiante nesta seção.
