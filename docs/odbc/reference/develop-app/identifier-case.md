---
title: Caso identificador | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300146"
---
# <a name="identifier-case"></a>Caso do identificador
Em declarações SQL e argumentos de função de catálogo, identificadores e identificadores citados podem ser sensíveis a maiúsculas ou não, o que um aplicativo pode determinar ligando para **o SQLGetInfo** com as opções de SQL_IDENTIFIER_CASE e SQL_QUOTED_IDENTIFIER_CASE.  
  
 Cada uma dessas opções tem quatro valores de retorno possíveis: um afirmando que o caso identificador ou citado é sensível e três afirmando que não é sensível. Os três valores que não são sensíveis a maiúsculas e minúsculas descrevem ainda o caso em que os identificadores são armazenados no catálogo do sistema. A forma como os identificadores são armazenados no catálogo do sistema é relevante apenas para fins de exibição, como quando um aplicativo exibe os resultados de uma função de catálogo; não altera a sensibilidade do caso dos identificadores.
