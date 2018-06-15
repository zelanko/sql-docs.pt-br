---
title: Identificador caso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 66218fb955a4133a5c689f72ab8f4b96504c9bd2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908841"
---
# <a name="identifier-case"></a>Identificador de caso
Em instruções SQL e argumentos de função de catálogo, identificadores e identificadores entre aspas podem ser diferencia maiusculas de minúsculas ou não, que um aplicativo pode determinar chamando **SQLGetInfo** com o SQL_IDENTIFIER_CASE e SQL_QUOTED_ Opções de IDENTIFIER_CASE.  
  
 Cada uma dessas opções tem quatro valores de retorno possíveis: um informando que o identificador ou identificador entre aspas caso confidencial e três informando que ele não é confidencial. Os três valores que não diferenciam maiusculas de minúsculas mais descrevem o caso em que os identificadores forem armazenados no catálogo do sistema. Como os identificadores forem armazenados no catálogo do sistema são relevante apenas para fins de exibição, como quando um aplicativo exibe os resultados de uma função de catálogo; ele não altera a diferenciação de maiusculas e minúsculas de identificadores.
