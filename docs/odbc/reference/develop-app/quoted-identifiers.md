---
title: Identificadores entre aspas | Microsoft Docs
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
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e74c39ad73357e50c1040e8a90029c0bf65f7b6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="quoted-identifiers"></a>Identificadores entre aspas
Em uma instrução SQL, os identificadores que contêm caracteres especiais ou correspondência de palavras-chave devem ser colocados entre *caracteres de aspas*; identificadores entre esses caracteres são conhecidos como *deidentificadoresentreaspas*(também conhecido como *identificadores delimitados* em SQL-92). Por exemplo, o identificador de contas a pagar é mencionado na tabela a seguir **selecione** instrução:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 O motivo para delimitar identificadores é fazer a instrução pode ser analisado. Por exemplo, se contas a pagar não estava entre aspas na instrução anterior, o analisador seria assumir duas tabelas, contas e a pagar e retornar um erro de sintaxe que não eram separados por uma vírgula. O identificador de caractere de aspas é específico do driver e é recuperado com a opção SQL_IDENTIFIER_QUOTE_CHAR na **SQLGetInfo**. A lista de caracteres especiais e palavras-chave é recuperada com as opções SQL_SPECIAL_CHARACTERS e SQL_KEYWORDS na **SQLGetInfo**.  
  
 Para ser seguro, aplicativos interoperáveis geralmente cotação todos os identificadores, exceto aqueles para pseudo colunas, como a coluna ROWID no Oracle. **SQLSpecialColumns** retorna uma lista de pseudo colunas. Além disso, se houver restrições específicas do aplicativo no qual os caracteres especiais podem aparecer em um nome de objeto, ele é ideal para aplicativos interoperáveis para não usar caracteres especiais em posições desses.
