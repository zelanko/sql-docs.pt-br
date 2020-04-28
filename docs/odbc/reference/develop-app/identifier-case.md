---
title: Caso de identificador | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940d96ece6b2c344fa02e0daadd6248270f4d19e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300146"
---
# <a name="identifier-case"></a>Caso do identificador
Em instruções SQL e argumentos de função de catálogo, identificadores e identificadores entre aspas podem diferenciar maiúsculas de minúsculas ou não, o que um aplicativo pode determinar chamando **SQLGetInfo** com as opções SQL_IDENTIFIER_CASE e SQL_QUOTED_IDENTIFIER_CASE.  
  
 Cada uma dessas opções tem quatro valores de retorno possíveis: um informando que o identificador ou o caso do identificador entre aspas é confidencial e três afirmando que ele não é confidencial. Os três valores que não diferenciam maiúsculas e minúsculas descrevem o caso em que os identificadores são armazenados no catálogo do sistema. Como os identificadores são armazenados no catálogo do sistema são relevantes apenas para fins de exibição, como quando um aplicativo exibe os resultados de uma função de catálogo; Ele não altera a diferenciação de maiúsculas e minúsculas dos identificadores.
