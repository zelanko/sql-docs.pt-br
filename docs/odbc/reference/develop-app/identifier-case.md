---
title: Identificador de caso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70728908f081ab89e08cad1265f04394f29b66ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138968"
---
# <a name="identifier-case"></a>Caso do identificador
Em instruções SQL e os argumentos de função de catálogo, identificadores e identificadores entre aspas podem ser diferencia maiusculas de minúsculas ou não, que um aplicativo pode determinar chamando **SQLGetInfo** com o SQL_IDENTIFIER_CASE e SQL_QUOTED_ Opções de IDENTIFIER_CASE.  
  
 Cada uma dessas opções possui quatro valores de retornados possíveis: um informando que o identificador de caso do identificador entre aspas é confidencial e três informando que não é confidencial. Os três valores que não diferenciam maiusculas de minúsculas descrevem ainda mais o caso em que os identificadores são armazenados no catálogo do sistema. Como os identificadores são armazenados no catálogo do sistema são relevante apenas para fins de exibição, como quando um aplicativo exibe os resultados de uma função de catálogo; ele não altera a diferenciação de maiusculas e minúsculas de identificadores.
