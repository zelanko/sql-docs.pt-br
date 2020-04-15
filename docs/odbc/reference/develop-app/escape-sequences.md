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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d9589230183b198cb7d59cf9739dab75625441e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298706"
---
# <a name="escape-sequences"></a>Sequências de escape
O ODBC define seqüências de fuga contendo gramática padrão para literals de data, hora, carimbo de data e intervalo de data, chamadas de função escalar, caracteres de fuga **de** predicado, junções externas e chamadas de procedimento. As aplicações interoperáveis devem usar essas seqüências sempre que possível.  
  
 Para determinar se um driver suporta as seqüências de escape para literals de data, hora, carimbo de data ou intervalo de data, um aplicativo chama **SQLGetTypeInfo**. Se a fonte de dados suportar um tipo de dados de data, hora, carimbo de data ou intervalo de data, ele também deve suportar a seqüência de fuga correspondente. Para determinar se as outras seqüências de fuga são suportadas, um aplicativo chama **SQLGetInfo**.  
  
 Para obter mais informações, consulte [Seqüências de fuga no ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md), mais tarde nesta seção.
