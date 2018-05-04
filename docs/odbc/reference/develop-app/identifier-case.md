---
title: Identificador caso | Microsoft Docs
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
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c709fa4512611dd67387583dd1bc1807402cece9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="identifier-case"></a>Identificador de caso
Em instruções SQL e argumentos de função de catálogo, identificadores e identificadores entre aspas podem ser diferencia maiusculas de minúsculas ou não, que um aplicativo pode determinar chamando **SQLGetInfo** com o SQL_IDENTIFIER_CASE e SQL_QUOTED_ Opções de IDENTIFIER_CASE.  
  
 Cada uma dessas opções tem quatro valores de retorno possíveis: um informando que o identificador ou identificador entre aspas caso confidencial e três informando que ele não é confidencial. Os três valores que não diferenciam maiusculas de minúsculas mais descrevem o caso em que os identificadores forem armazenados no catálogo do sistema. Como os identificadores forem armazenados no catálogo do sistema são relevante apenas para fins de exibição, como quando um aplicativo exibe os resultados de uma função de catálogo; ele não altera a diferenciação de maiusculas e minúsculas de identificadores.
